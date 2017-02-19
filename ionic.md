IONIC
=====

> Ionic is the beautiful, free and open source mobile SDK for developing native and progressive web apps with ease.

* http://ionic.io


Install Ionic
-------------

```
$ npm install -g cordova ionic
$ ionic --version
```

Start an App
------------

```
$ ionic start myApp blank 
$ ionic start myApp tabs 
$ ionic start myApp sidemenu 
```

Run your App
------------

Run your app in the browser (great for initial development):
```
$ ionic serve 

http://192.168.0.21:8100
```

```
$ ionic serve --lab

http://192.168.0.21:8100/ionic-lab
```

배포
----

```
$ ionic login 
```

```
$ ionic upload 
```

If you’ve previously created an app on the Dashboard and you want to sync a local project, set the app ID in the `ionic.config.json` file.  
```
{
  "name": "hint",
  "app_id": "544fbbc9"
}
```

Run on a device or simulator:
```
ionic run ios[android,browser]
```

Share your app with testers, and test on device easily with the Ionic View companion app:
```
http://view.ionic.io
```

참고
----

* http://ionicframework.com/getting-started/
* http://blog.jeonghwan.net/2016/08/03/ionic-hello-world.html