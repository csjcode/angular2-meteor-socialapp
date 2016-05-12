
### Problems & Solutions (in order encountered)

There were a number of configuraton proproblems



--------------- PROBLEM [solved] ---------------



https://forums.meteor.com/t/angular-meteor-com-angular2-tutorial-mongo-namespace-error/19722
I finished the 3rd section of the tutorial and everything is working fine, live updating from Mongo insertions and everything, but I receive the following error while meteor is running.

[web.browser] client/app.ts (14, 12): Cannot find namespace 'Mongo'.
[web.browser] collections/players.ts (1, 26): Cannot find name 'Mongo'.
[os.osx.x86_64] server/main.ts (3, 1): Cannot find name 'Meteor'.

EDIT: Fixed it.

At some point I messed up and over-wrote my typings folder, removing the main.d.ts file that was generated.

Just rerun:

npm install typings -g
typings install meteor --ambient
typings install es6-promise --ambient
typings install es6-shim --ambient




--------------- PROBLEM [solved] ---------------



[SOLVED] Meteor angular2 : import {Meteor} from ‘meteor/meteor’; cannot find module
https://forums.meteor.com/t/solved-meteor-angular2-import-meteor-from-meteor-meteor-cannot-find-module/20985

Please look at the end of the first chapter. it links to that gist here - https://gist.github.com/tomitrescak/8366ce98f1857e202ea885 which is an updated version of the Meteor typings for Meteor 1.3
let me know if that works for you

rebolon
Apr 12

So i copy/paste the gist into a meteor.d.ts at the root of my app, and it worked well, thanks a lot @Urigo

Do you know why i have to deal with that file ? Is it mandatory for all meteor 1.3 application ?

Thanks a lot for your work on meteor/angularX



--------------- PROBLEM [solved] ---------------



For some reason I wasn''t including:
 import {Component, NgZone} from 'angular2/core';

 So was getting an error that NgZone wasn't found.



--------------- SECTON 3.7 PROBLEM [solved] ---------------



https://forums.meteor.com/t/for-people-who-are-following-socially-tutorial-and-met-problems/22994
To run Angular 2 RC1 and Meteor 1.3 successfully, you need:

    Remove your old Angular 2 if you are using Angular 2 Beta version:
    npm uninstall --save angular2

    And run this to install Angular RC 1:
    npm install --save @angular/core @angular/common @angular/platform-browser @angular/platform-browser-dynamic @angular/router-deprecated

    When you import, use new one:
    1) Change
    import { Component } from 'angular2/core';
    to
    import { Component } from '@angular/core';
    2) Change
    import { bootstrap } from 'angular2/platform/browser';
    to
    import { bootstrap } from '@angular/platform-browser-dynamic'; // use this if you do not use meteor features
    or
    import { bootstrap } from 'angular2-meteor-auto-bootstrap'; // use this if you use meteor features
    Check here2 for the rest of them.

    Change
    *ngFor="#party of parties"
    to
    *ngFor="let party of parties"
