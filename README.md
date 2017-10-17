Redirect account.openshift.com
===============
Redirect account.openshift.com using Apache via the [PHP](http://www.php.net) 
builder image on OpenShift.

Repository Organization
----------------------------------
You do not need to change anything in your existing PHP project's repository.
However, some files will affect the behavior of the build process:

```
.htaccess            Apache .htaccess file <1>
.s2i/                     
    environment      Environment variables file <2>
```
1. See the Apache Configuration section below
2. See the Environment Variables section below


Apache Configuration
----------------------------------
In case the **DocumentRoot** of the application is nested within the source directory `/opt/app-root/src`,
users can provide their own Apache **.htaccess** file.  This allows the overriding of Apache's behavior and
specifies how application requests should be handled. The `.htaccess` file needs to be located at the root
of the application source.


Environment Variables
----------------------------------
The PHP image supports a number of environment variables which can be set to
control the configuration and behavior of the PHP runtime.

To set these environment variables as part of your image, you can place them into
[a *_.s2i/environment_* file](https://docs.openshift.org/latest/dev_guide/builds.html#environment-files)
inside your source code repository, or define them in
[the environment section](https://docs.openshift.org/latest/dev_guide/builds.adoc#buildconfig-environment) of the build configuration's `*sourceStrategy*` definition.

You can also set environment variables to be used with an existing image when
[creating new applications](https://docs.openshift.org/latest/dev_guide/application_lifecycle/new_app.html#specifying-environment-variables), or by
[updating environment variables for existing objects](https://docs.openshift.org/latest/dev_guide/environment_variables.html#set-environment-variables) such as deployment configurations.

> **Note:** Environment variables that control build behavior must be set as part of the S2I build configuration or in the *_.s2i/environment_* file to make them available to the build steps.

Hot deploy
----------------------------------
In order to immediately pick up changes made in your application source code, you need to run your built 
image with the `OPCACHE_REVALIDATE_FREQ=0` environment variable.