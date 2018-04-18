### Code for "LocalSettings.php" for using the Datencockpit flavour to the MediaWiki Chameleon skin

```php
# Chameleon
// Composer
$egChameleonLayoutFile = __DIR__ . '/skins/Datencockpit/datencockpit.xml';
$egChameleonExternalStyleModules = [
	__DIR__ . '/skins/Datencockpit/bootswatch.less' => $wgScriptPath,
	__DIR__ . '/skins/Datencockpit/variables.less' => $wgScriptPath,
	__DIR__ . '/skins/Datencockpit/datencockpit.less' => $wgScriptPath
	];
$egChameleonExternalLessVariables = [
	'container-large-desktop' => '100%;',
	'navbar-height' => '40px',
	'table-condensed-cell-padding' => '4px',
	'navbar-default-bg' => 'rgba( 99, 141, 187, 1 )',
  'dropdown-link-hover-bg' => 'rgba(99, 141, 187, 1)',
	];

\Bootstrap\BootstrapManager::getInstance()->addCacheTriggerFile(
  [ 'datencockpit.less' => __DIR__ . '/datencockpit.less' ]
  );

$wgHooks[ 'ChameleonNavbarHorizontalPersonalToolsLinkText' ][] = function ( &$linkText, SkinChameleon $skin ) {
    $userImages = \SMW\StoreFactory::getStore()->getPropertyValues( \SMW\DIWikiPage::newFromTitle( $skin->getUser()->getUserPage() ), \SMW\DIProperty::newFromUserLabel( 'User image' ) );
    if ( !empty( $userImages ) ) {
        $userImage = reset( $userImages );
        if ( is_a( $userImage, '\SMW\DIWikiPage' ) && $userImage->getNamespace() === NS_FILE ) {
            $imagePage = new WikiFilePage( $userImage->getTitle() );
            $linkText = '<img src="' . $imagePage->getFile()->createThumb( 41, 41 ) . '">';
        }
    }
    return true;
};

## Default skin
$wgDefaultSkin = 'chameleon';
```
