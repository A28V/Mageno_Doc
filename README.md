# Mageno_Doc

composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition magento23



After run this command:

change in vendor folder (if you are installing magento on local-windown-system)

ERROR1. php setup:upgrade time error:

	"In PatchApplier.php line 170:

	  Unable to apply data patch Magento\Theme\Setup\Patch\Data\RegisterThemes for module Magento_Theme. Original exception message: Wrong file
	 
	In Gd2.php line 64"
Soluction1.1:
    GO TO file path: "E:\xampp2\htdocs\magento26\vendor\magento\framework\Image\Adapter\Gd2.php
    changes: 
	---------
	before:
		 private function validateURLScheme(string $filename) : bool
		 {
			 $allowed_schemes = ['ftp', 'ftps', 'http', 'https'];
			 $url = parse_url($filename);
			 if ($url &amp;&amp; isset($url['scheme']) &amp;&amp; !in_array($url['scheme'], $allowed_schemes)) {
				 return false;

	--------
	after:     private function validateURLScheme(string $filename) : bool
		 {
			 $allowed_schemes = ['ftp', 'ftps', 'http', 'https', 'C']; // <Your_drive_name for example C>
			 $url = parse_url($filename);
			 if ($url &amp;&amp; isset($url['scheme']) &amp;&amp; !in_array($url['scheme'], $allowed_schemes)) {
				 return false;

ERROR2: di:compile time error:
    Warning: file_put_contents(F:/xampp/htdocs/magento/generated/metadata/prima
	 ry|global|plugin-list.php): failed to open stream: No such file or director
	 y in F:\xampp\htdocs\magento\vendor\magento\framework\Interception\PluginLi
	 stGenerator.php on line 414
Solution2.1: Replace the line
				$cacheId = implode('|', $this->scopePriorityScheme) . "|" . $this->cacheId;
				
			with below:
				$cacheId = implode('-', $this->scopePriorityScheme) . "-" . $this->cacheId;
ERROR3: 404 error(page not found):
          How to Resolve Blank page Issue after installing Magento 2.x,
Solution3.1: E:\xampp2\htdocs\magento2\vendor\magento\framework\View\Element\Template\File\validator.php
        Search this function function isPathInDirectories()
		and inside You can see
		$realPath = $this->fileDriver->getRealPath($path);
		 And replace it with the below code.

		 $realPath = str_replace('\\', '/', $this->fileDriver->getRealPath($path));
		 That’s it now open your command line interface (CLI) and run following command.
 
			php bin/magento cache:clean
			php bin/magento cache:flush
			php bin/magento indexer:reindex
			php bin/magento setup:upgrade
			php bin/magento setup:static-content:deploy -f
			
After complete overall changes, create --host:

         How to create virtual-host
                go to this path C:\Windows\System32\drivers\etc\hosts
                       127.0.0.1 local_server.com
                after that, go to E:\xampp2\apache\conf\extra\httpd-vhosts.conf
				     <VirtualHost *:80>
						ServerAdmin "local_server.com"
						DocumentRoot "E:\xampp2\htdocs\magento2\pub" ## your magento project path
						ServerName "local_server.com"
					 </VirtualHost>
                    				

 After that, run following command


php bin/magento setup:install --base-url="http://magento23.com/" --db-host="localhost" --db-name="magento2" --db-user="root" --db-password="" --admin-firstname="Admin" --admin-lastname="Admin" --admin-email="admin@admin.com" --admin-user="admin" --admin-password="admin123" --use-rewrites="1" --backend-frontname="admin" --db-prefix=mage_


Error4: SOLVED - Magento 2 - Unable to login to admin (no error message) stuck at login screen

solution4.1:
    If Your domain is secure then add the https:// in you domin otherwise you add the http:// only web/unsecure/base_url => 'https://yoursiteurl.com/'

    web/secure/base_url => 'https://yoursiteurl.com/'

    php -f bin/magento setup:upgrade

    php -f bin/magento setup:static-content:deploy en_US -f

    php -f bin/magento cache:flush

    clear your Browser cookies and cache



Errror5: Failed to send the message. Please contact the administrator

soluction php bin/magento module:disable




------------------------------------------------------------------------------------------------------------

All Magenton command 


php bin/magento setup:upgrade
php bin/magento setup:di:compile
php bin/magento setup:static-content:deploy -f en_US it_IT


php -f bin/magento cache:flush
 
php bin/magento module:enable Test_Arun 
php bin/magento module:disable Test_Arun 
php bin/magento module:status

php bin/magento indexer:reindex
php bin/magento cache:clean
php bin/magento cache:flush



php bin/magento setup:static-content:deploy -f en_US it_IT
php bin/magento setup:upgrade
php bin/magento setup:db-schema:upgrade

php bin/magento setup:di:compile
php bin/magento cache:clean
php bin/magento cache:flush
php bin/magento setup:static-content:deploy -f

php bin/magento maintenance:enable 

php bin/magento maintenance:disable 

php bin/magento setup:static-content:deploy en_CA it_IT

php bin/magento indexer:reindex

    find . -type f -exec chmod 644 {} \;            
    find . -type d -exec chmod 755 {} \;        
    mkdir  -Rf 777 var
    mkdir  -Rf 777 pub/static
    mkdir  -Rf 777 pub/media
    mkdir  777 ./app/etc
    mkdir  644 ./app/etc/*.xml
    mkdir  -Rf 775 bin
	
php bin/magento setup:install --base-url="test.arun.com"--db-host="167.99.205.158"--db-name="zayron"--db-user="root"--db-password="" --admin-firstname="Admin"--admin-lastname="Admin"--admin-email="arunsuryavanshi1111@gmail.com"--admin-user="mysupportteam"--admin-password="support@234" --use-rewrites="1"--backend-frontname="admin"--db-prefix=mage_

COMPOSER_MEMORY_LIMIT=-1 composer create-project 

memory issue :

php -d memory_limit=-1 E:\composer\composer.phar require --repository-url=https://repo.magento.com/ magento/project-community-edition:2.4.5 
php bin/magento admin:user:create --admin-user="mysupportteam" --admin-password="support@234" --admin-email="arunsuryavanshi1111@gmail.com" --admin-firstname="Admin" --admin-lastname="Admin"
