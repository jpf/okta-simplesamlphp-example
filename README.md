# Introduction

This is an example PHP application that makes use of the
[SimpleSAMLphp](https://simplesamlphp.org/) library support Single Sign-On with SAML.

# Requirements

This example application depends on SimpleSAMLphp being installed in
"../simplesamlphp". Meaning, this example expects SimpleSAMLphp to
be installed one level up from this example in a folder called
"simplesamlphp".

# Setting up Okta

Before you can configure your application SimpleSAMLphp you 
will need to set up an Okta "[chiclet](https://support.okta.com/articles/Knowledge_Article/27838096-Okta-Terminology)" (application icon) that enables an Okta 
user to sign in to your to your application with SAML and SimpleSAMLphp.

To set up Okta to connect to your application, follow the
[setting up a SAML application in Okta](http://developer.okta.com/docs/guides/setting_up_a_saml_application_in_okta.html) guide. 
As noted in the instructions, there are two steps to change:

**In step #6**: 

Use "SimpleSAMLphp Example" instead of "Example SAML application".

**In step #7**: 

When entering the URL

```
http://example.com/saml/sso/example-okta-com
```

instead, use the following:

For "Single sign on URL" use:

```
http://PATH_TO_INSTALL_DIRECTORY/simplesamlphp/www/module.php/saml/sp/saml2-acs.php/example
```

For "Audience URI (SP Entity ID)" use:

```
http://PATH_TO_INSTALL_DIRECTORY/simplesamlphp/www/module.php/saml/sp/metadata.php/example
```

For "Default RelayState" use:

```
http://PATH_TO_INSTALL_DIRECTORY/okta-simplesamlphp-example/?saml_sso=example
```

**Note:**
"PATH\_TO\_INSTALL\_DIRECTORY" is the full path to the directory where SimpleSAMLphp and this application reside.
It might look like: "example.com" or might contain a path like "example.com/path". 
This will depend on how your webserver is set up.

# Setting up SimpleSAMLphp

1.  Use \`git clone\` to pull down this git repository.
2.  Copy the \`saml-autoconfig.php\` file to the directory for SimpleSAMLphp.
    Assuming that you cloned this repository to the same level as
    SimpleSAMLphp, this is the command you will use to do this:
    
    ```shell 
    $ cp okta-simplesamlphp-example/saml-autoconfig.php simplesamlphp/ 
    ```
3.  In the 'simplesamlphp' directory, 
    edit the \`config/authsources.php\` 
    and \`metadata/saml20-idp-remote.php\` files and add the line below to each file:
    
    ```php
    require(dirname(__FILE__).'/../saml-autoconfig.php');
    ```
4.  Finally, open the \`saml-autoconfig.php\` file in your favorite text editor.
    In the \`$metadata\_url\_for\\\` array, add an entry where the key is a
    string like "example" and the value is the metadata URL you got
    from the "Setting up Okta" section above. It should look like this:
    
    ```php
    $metadata_url_for = array(
        'example' => 'https://example.okta.com/app/abc0de1fghIjKlMNo2p3/sso/saml/metadata',
    );
    ```

# Testing

1.  Load the URL for \`okta-simplesamlphp-example/index.php\` in your web browser. 
    Try to log in to the 'example' IdP.
2.  In Okta, try clicking on the "SimpleSAMLphp Example" chiclet.

# Contact

Updates or corrections to this document are very welcome. Feel free
to send me [pull requests](https://help.github.com/articles/using-pull-requests/) with suggestions.


Additionally, please send me comments or questions via email: &#106;&#111;&#101;&#108;&#046;&#102;&#114;&#097;&#110;&#117;&#115;&#105;&#099;&#064;&#111;&#107;&#116;&#097;&#046;&#099;&#111;&#109;