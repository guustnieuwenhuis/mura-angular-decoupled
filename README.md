# MuraAngularDecoupled

## Initial Startup

First you need to start Mura up:
```
git clone https://github.com/murasoftware/mura-angular-decoupled.git
cd mura-angular-decoupled
git checkout master
docker-compose up
```

Then go to http://localhost:8888 to initialize Mura's install then login with the default (admin/admin) and edit the default site's settings:
* Domain= The domain of the remote site that the the content will be served on. (localhost)
* Is Remote = true
* Remote Context = The directory structure off of the remote site's web root that the site lives (Leave Empty)
* Remote Port = The port of the remote site (4200)
* Resource Domain = The domain that Mura will use the access resource like css and js scripts that are dynamically loaded. (localhost)

Second you need to start Angular up:

If you haven't already install Angular CLI you will need to run This

```
npm install -g @angular/cli
```

Then in terminal install the Angular application:
```
npm install
```

If you're on Windows you will need to edit this file to change "cp" to "copy"

https://github.com/murasoftware/mura-angular-decoupled/blob/master/package.json#L20

Then start the Angular service

```
npm run start
```

You can now visit the site at http://localhost:4200

And finally go to your Mura admin (http://localhost:8888/admin) and reload Mura one more to and it will see the mura.config.json from the ./angular directory.

# Key Points of Integration with Mura

The intergration is entirely done with Mura.js installed as an npm within the and project while running Mura's official docker container.

## Mura Version

You must use Mura 7.1.324 of higher

## NPM
https://www.npmjs.com/package/mura.js

## Mura.js documentation

https://docs.getmura.com/v7-1/mura-developers/mura-rendering/murajs/

## Docker Image

https://hub.docker.com/r/murasoftware/mura

## Theming

With this use case Mura modules, templates and content type includes are now located outside of Mura within the client.

https://github.com/murasoftware/mura-angular-decoupled/tree/master/src/app/contenttypes/default
https://github.com/murasoftware/mura-angular-decoupled/tree/master/src/app/templates
https://github.com/murasoftware/mura-angular-decoupled/tree/master/src/app/modules

## Configuring Mura Remotely

There is a mura.config.json file that the Mura service reads in when loading to get what it needs to know from the client.

https://github.com/murasoftware/mura-angular-decoupled/blob/master/mura.config.json

You tell Mura about it as an environment variable

https://github.com/murasoftware/mura-angular-decoupled/blob/master/docker-compose.yml#L22

When Angular starts up is get's copied to the public /assets Directory

https://github.com/murasoftware/mura-angular-decoupled/tree/master/src/assets

Mura.js is initialized from within the mura.service file that also wires in any custom modules

https://github.com/murasoftware/mura-angular-decoupled/blob/master/src/app/mura.service.ts

## Mura ORM Assembler and Scaffolder

An important aspect of Mura 7.1 and this new way of working with Mura is using the Mura ORM Assembler and Scaffolder to create your own custom entities.  You can then use Mura.js to seamlessly access them within your client.  It works the same way as working with normal content and feeds.

https://docs.getmura.com/v7-1/mura-developers/mura-beans-objects/custom-objects/mura-orm/mura-orm-assembler-scaffolder/

## Mura Module Configurator Markup Conventions

https://docs.getmura.com/v7-1/mura-ui-markup-conventions/custom-module-display-object-configurators/

# Key Points About Angular

This demonstration project does not currently support prerendering or ssr.