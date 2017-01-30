Site:
=======
 - Site / Domain Name - URL (http://www.example.com/)
 - Build - PHP _and_ (Version Number)
 - ( CMS / Development URL's and Info. -  _IF NEEDED_ )

    CMS URL:  http://www.example.com/

    Username:  user

    Password:  password

 - ( Development Site Info. -  _IF NEEDED_ )

    DEV URL:  http://dev.example.com/

 HOSTING / REGISTRAR:
 ====================
 - Hosting - [Service Name w/ link](link) ( Paid / Free )
 - Domain Registrar - [Service Name w/ link](link) ( Paid / Free )

 SERVICES:
 =========

 ( Heroku Services )

 - Web Service - App Type w/ # of dynos ( Paid / Free )
 - Any Heroku Add-on Service - [Service Name w/ link](link) ( Paid / Free )

 ( Other Services )

 - Database Type - MySQL / MongoDB
 - Database Service - [Service Name w/ link](link) ( Paid / Free )
 - SSL Certificate Service - [Service Name w/ link](link) ( Paid / Free )
 - CDN - [Service Name w/ link](link) ( Paid / Free )
 - Site Monitor / Debugging / Logging Service - [Service Name w/ link](link) ( Paid / Free )
 - Email Service - [Service Name w/ link](link) ( Paid / Free )
 - Site Analytics - [Service Name w/ link](link) Tracking ID: UA-00000-1 ( Paid / Free )
 - Any Additional Service - [Service Name w/ link](link) ( Paid / Free )

 REQUIREMENTS:
 ==============
 ( PHP Basic Template: _STRUCTURE AND SETUP_ )

 ### Folder & Directory Structure:

```
/ (project root)
├── mockups/ ( PSD / EPS GRAPHICS FILES )
├── working/ ( PSD / EPS GRAPHICS FILES )
├─┬ www/ (web root)
│ ├─┬ assets/ (All site assets and scripts)
│ │ ├── images/
│ │ ├── scripts/
│ │ └── styles/
│ ├── libs/ (Any extra libraries or scripts)
│ ├── pieces/ (The helper files directory)
│ ├── partials/ (Directory of any server-side includes)
│ ├── templates/
│ ├── .htaccess (Apache config and re-write rules)
│ ├── config.php (Site-wide Database Connection values)
│ └── index.php
├── .gitignore
├── .slugignore (Heroku ignored files and directories)
├── Procfile (Heroku Config File)
└── composer.json (Additional Tools and dependency)
```

 **Directory / File Descriptions:**

  **libs** : _This directory is where we place extra PHP (or JavaScript) libraries. Typically these sort of tools/dependencies are now installed via Composer.  However, there are times when it's beneficial to store authentication or self-defined tools here._

  **pieces** : _This directory is where all the helper and database usability files are stored.  The_ **helpers.php** _file contains a helpers class, along with a series of public functions that help display the template-based pages and other useful functions to make coding easier.  The_ **msqliData.php** _has several pre-defined MySQL queries to help in accessing data and displaying it on a page easier._

  **templates** : _Where the page templates for the site are stored. Typically, the page templates are the outer shell of the page (containing the_ **HTML, HEAD & BODY** _tags). The stylesheets, JavaScripts and any analytics tags are placed in the template files. The individual pages themselved (_ **IE - index.php** _) define the interior content of each the page._

  **config.php** : _This file serves a couple different functions.  First, it is used to establish the site directory/file_ **BASE** _via the helpers.php file. It also servers as the main file to define_ **$GLOBAL** _variables for the site. The most important global variables that are defined are the_ **$PIECES** _which are used to define the database connection values for authentication.  This file can also be used to define session names and error reporting for development enviorments._



### Other Tools & Dependencies:

  **Swiftmailer** : _A free, feature-rich PHP mailer. Swift Mailer integrates into any web app written in PHP 5, offering a flexible object-oriented approach to sending emails with a multitude of features. We have used Swift Mailer on previous projects with good results.  Swift Mailer's library can be installed using Composer._

  [Documentation](http://swiftmailer.org/docs/introduction.html)

  **Example:**

```
// Adding vendor autoload to access the Swift Mailer vendor
require_once 'vendor/autoload.php';

// Setting up the SMTP server, port, SSL, email-username and password
$transport = Swift_SmtpTransport::newInstance('smtp.gmail.com', 465, "ssl")
              ->setUsername('user@gmail.com')
              ->setPassword('password');

// Setting the mailer instance
$mailer = Swift_Mailer::newInstance($transport);

// Defining who the message is from, who it's going to and the message body
$message = Swift_Message::newInstance('New Message')
						  ->setFrom(array('user@gmail.com' => 'From Email Common Name'))
						  ->setTo(array('to-email@gmail.com'))
						  ->setBody('Put The Email Message Here');

// Sending the message
$result = $mailer->send($message);
```

 **Rackspace/PHP-Opencloud** : _A Rackspace library for PHP that offers a wide range of services.  We have used the_ **object-store** _service for uploading images and assets to Rackspace containers._

 [Object-store Documentation](http://docs.php-opencloud.com/en/latest/services/object-store/index.html)

 **Example: upload-object.php**

 ```
 // Adding the vendor autoload.php and accessing the php-opencloud vendor
 require dirname(__DIR__) . '/../vendor/autoload.php';
 use OpenCloud\Rackspace;

 // 1. Instantiate a Rackspace client. You can replace {authUrl} with
 // Rackspace::US_IDENTITY_ENDPOINT or similar
 $client = new Rackspace(Rackspace::US_IDENTITY_ENDPOINT, array(
     'username' => 'username',
     'apiKey'   => 'apikey',
 ));

 // 2. Obtain an Object Store service object from the client.
 $objectStoreService = $client->objectStoreService(null, 'DFW');

 // 3. Get container.
 $container = $objectStoreService->getContainer('container-name');

 // 4. Check if the file exists in Rackspace
 $exists = $container->objectExists($values["image"]);

 // 5. Open local file
 $fileData = fopen($_FILES["image"]["tmp_name"], 'r');

 // 6. Upload it! Note that while we call fopen to open the file resource, we do
 // not call fclose at the end. The file resource is automatically closed inside
 // the uploadObject call.
 if(!isset($exists) || $exists == false) {
   $container->uploadObject($values["image"], $fileData);
 }
 
 ```
