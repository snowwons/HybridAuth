# OrgHeiglHybridAuth

[![Build Status](https://travis-ci.org/heiglandreas/HybridAuth.png?branch=master)](https://travis-ci.org/heiglandreas/HybridAuth)
[![Latest Stable Version](https://poser.pugx.org/org_heigl/hybridauth/v/stable.png)](https://packagist.org/packages/org_heigl/hybridauth)
[![Total Downloads](https://poser.pugx.org/org_heigl/hybridauth/downloads.png)](https://packagist.org/packages/org_heigl/hybridauth)
[![Stories in Ready](https://badge.waffle.io/heiglandreas/HybridAuth.png?label=ready)](https://waffle.io/heiglandreas/HybridAuth)  


Use the HybridAuth-Library to create an absolute lightweight Authentication-Layer
for your ZendFramework2-App

You can login with all [supported SocialNetwork-Logins](http://hybridauth.sourceforge.net/userguide.html).
The network and a user-object holding id, name, mail and language will be stored in the session. If you already have
SocialNetwork users in your application you can use these to authorize your users.

## Requirements

* The [hybridAuth-library](http://hybridauth.sourceforge.net)
* Zend Framework2 (well, obvious, isn't it?)

## Usage

1. In your application.conf-file add the Module to the list of modules
2. Copy the file ```vendor/org_heigl/hybridauth/config/autoload/module-orgHeiglHybridAuth.local.php``` to your
    applications ```config/autoload```-directory and adapt as appropriate.
3. Add this snippet to create a login-link

    ```php
    <?php
    $provider = "Twitter";
    echo $this->hybridauthinfo($provider);
    ?>
    ```

4. After login you can access the user-info the following way:

    ```php
    $config = $this->getServiceLocator()->get('Config');
    $config = $config['OrgHeiglHybridAuth'];
    $hybridAuth = new Hybridauth($config['hybrid_auth']);

    $token = $this->getServiceLocator()->get('OrgHeiglHybridAuthToken');
    if (! $token->isAuthenticated()) {
        echo 'No user logged in';
    }
    /** @var OrgHeiglHybridAuth\UserToken $user */
    echo $token->getName(); // The name of the logged in user
    echo $token->getUID();  // The internal UID of the used service
    echo $token->getMail(); // The mail-address the service provides
    echo $token->getLanguage(); // The language the service provides for the user
    echo $token->getService()  // Should print out the Name of the service provider.
    ```

## Installation

This module is best installed using [composer](http://packagist.org/packages/org_heigl/hybridauth). For that, add the
following line to the ```require```-section of your ```composer.json```-file and run composer.

    "org_heigl/hybridauth": "dev-master"

Alternatively you can fork the project at [github](https://github.com/heiglandreas/OrgHeiglHybridAuth).
