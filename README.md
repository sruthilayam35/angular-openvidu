# angular-openvidu
[![Travis][travis-image]][travis-url]
[![Dependency Status][dependency-status-image]][dependency-status-url]
[![Angular style guide][codelyzer-image]][codelyzer-url]
[![GitHub license][license-image]][license-url]

**AngularOpenVidu** is a room videoconference component library for [Angular](https://angular.io/).

It's written in [TypeScript](https://www.typescriptlang.org/), with the guidelines from [Angular Style Guide](https://angular.io/styleguide).

To be able to work in the browser, AngularOpenVidu uses [openvidu-browser][openvidu-browser] to communicate with the [OpenVidu Server][openvidu-server].

To use AngularOpenVidu, [WebRTC](https://en.wikipedia.org/wiki/WebRTC) support is required (Chrome, Firefox, Opera).

### Table of contents

- [App Demo](#demo)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Structure](#structure)
	- [Component Tree](#component-tree)
	- [File Structure](#file-structure)
- [API](#api)
	- [OpenViduDirective](#openvidudirective)
	- [OpenViduHangoutsComponent](#openviduhangoutscomponent)
	- [OpenViduAppearinComponent](#openviduappearincomponent)
- [Development](#development)
	- [Dependencies](#1-depedencies)
	- [CSS](#2-css)
	- [Tests](#3-tests)
- [Changelog](#changelog)
- [Troubleshooting](#troubleshooting)
- [License](#license)

### App Demo

In this demo you will see a use case of `angular-openvidu`, where you can test ALL the features included in this component.

Follow the instructions from the [app's README][angular-openvidu-demo] to test it out.

Link to the repository: [https://github.com/alxhotel/angular-openvidu-demo][angular-openvidu-demo]

### Features

- Join a group call
- Close group call
- Disable camera
- Mute microphone
- Toggle fullscreen video
- Send messages to the participants of the call

### Installation

1. Install `angular-openvidu` node module through npm:

	```bash
	$ npm install angular-openvidu --save
	```

2. Import `OpenViduModule` to your AppModule

	```js
	import { NgModule } from '@angular/core';
	import { BrowserModule  } from '@angular/platform-browser';
	import { FormsModule } from "@angular/forms";
	import { AppComponent } from './app.component';

	import { OpenViduModule } from 'angular-openvidu';

	@NgModule({
	  imports: [ BrowserModule, FormsModule, OpenViduModule ],
	  declarations: [ AppComponent ],
	  bootstrap: [ AppComponent ]
	})
	export class AppModule { }
	```

	You may also find it useful to view the [demo source](https://github.com/alxhotel/angular-openvidu-app/blob/master/src/app/app.component.ts).

3. Add `hammer.js` in your html:

	```html
	<script src="../node_modules/hammerjs/hammer.js"></script>
	```

4. Deploy OpenVidu Server

	You will need a [OpenVidu Server][openvidu-server].

	Follow the instructions in [this page](https://github.com/OpenVidu/openvidu-sample-basic-plainjs#start-openvidu-development-server) to deploy it with docker.

### Usage

You are ready. Use it in your template:

```html
<openvidu [wsUrl]="wsUrl" [sessionId]="sessionId" [participantId]="participantId">
	Loading openvidu...
</openvidu>
```

| Name | Type | Optional | Description |
|---|---|---|---|
| `wsUrl`			| `String` | required | Websocket URL pointing to your [OpenVidu Server][openvidu-server] |
| `sessionId`		| `String` | required | An id for the session you want to join to |
| `participantId`	| `String` | required | An id for the current participant joining the session |


*Note: `openvidu` is a selector for the [OpenViduHangoutsComponent](#openviduhangoutscomponent).*

### Structure

#### Component Tree

Below outlines a tree of how the components are arranged in the Angular component tree.

<p align="center"><img src="https://github.com/alxhotel/angular-openvidu/blob/master/docs/screenshots/component_tree.png?raw=true"/></p>

#### File Structure

The folder structure is aimed to encapsulate components into their own modules.
In each component folder, it contains all the html, css, js for that component. 

```
└── src
    ├── openvidu-template	-- root		directive with all the OpenVidu logic
    ├── openvidu-hangouts	-- root		component with a predefined layout for Hangouts
    │   └── stream-hangouts	-- stream	component for the Hangouts layout
    └── openvidu-appearin	-- root		component with a predefined layout for AppearIn
        └── stream-appearin	-- stream	component for the AppearIn layout
```

### API

AngularOpenVidu has multiple predefined layouts that you can use out-of-the-box.

#### OpenViduDirective

The OpenViduDirective is used to build components for controlling your video chat instance.
The directive selector is `openvidu-template`, either as an element or an attribute.
It exports an API named "openviduApi", which can then be used to build the video chat component.

[Click here to see the documentation](src)

#### OpenViduHangoutsComponent

*This is the default component for creating a video chat.*

It is implemented on top of the `OpenViduDirective`, and has a pre-set template and styles based on [Google Hangouts](https://hangouts.google.com).
If you require a more customised video chat, you will need to use the `OpenViduDirective` and implement your own component.

[Click here to see the documentation](src/openvidu-hangouts)

<img width="250" src="https://github.com/alxhotel/angular-openvidu/blob/master/docs/screenshots/openvidu_hangouts.png?raw=true"/>

#### OpenViduAppearinComponent

It is implemented on top of the `OpenViduDirective`, and has a pre-set template and styles based on [AppearIn](https://appear.in).
If you require a more customised video chat, you will need to use the `OpenViduDirective` and implement your own component.

[Click here to see the documentation](src/openvidu-appearin)

<img width="250" src="https://github.com/alxhotel/angular-openvidu/blob/master/docs/screenshots/openvidu_appearin.png?raw=true"/>

### Development

To compile, just run:

```bash
$ npm run build
```

Then, you will see the module compiled in the `dist` folder.

Things you need to know before contributing to this project:

#### 1. Dependencies

These are the main modules that make up AngularOpenVidu:

| Module | Version | Description |
|---|---|---|
| [OpenVidu Browser](openvidu-browser)		| [![][openvidu-browser-ni]][openvidu-browser-nu]		| used to communicate with the OpenVidu Server				|
| [Angular Material](@angular/material)		| [![][@angular/material-ni]][@angular/material-nu]		| used to display the toolbar, buttons and animations		|
| [Angular BigScreen](bigscren)				| [![][bigscreen-ni]][bigscreen-nu]						| used to toggle the fullscreen mode of the streaming		|

[openvidu-browser]: https://github.com/OpenVidu/openvidu/tree/master/openvidu-browser
[openvidu-browser-ni]: https://img.shields.io/npm/v/openvidu-browser.svg
[openvidu-browser-nu]: https://www.npmjs.com/package/openvidu-browser

[@angular/material]: https://github.com/angular/material2
[@angular/material-ni]: https://img.shields.io/npm/v/@angular/material.svg
[@angular/material-nu]: https://www.npmjs.com/package/@angular/material

[bigscreen]: https://github.com/alxhotel/angular-bigscreen
[bigscreen-ni]: https://img.shields.io/npm/v/angular-bigscreen.svg
[bigscreen-nu]: https://www.npmjs.com/package/angular-bigscreen

#### 2. CSS

The CSS stylesheet is compiled from the [LESS](http://lesscss.org/) files with a custom [gulp file](http://gulpjs.com/)

To build the LESS files just run:

```sh
$ gulp css
```

If you want to build the LESS files automatically every time there is a change, then run:

```sh
$ gulp watch
```

#### 3. Tests

To test the component run:

```sh
$ npm run test
```

### Changelog

You can find it [here](CHANGELOG.md).

### Troubleshooting

#### Why does it keep saying "Connecting..."?

You may be having some trouble connecting to the OpenVidu Server's websocket.

To make sure you are accepting its certificate go to:

- `[IP]`: Openvidu Server IP
- `[PORT]`: Openvidu Server port

```
https://[IP]:[PORT]/room
```

And make sure to accept its certificate. Then go back to the app and refresh the page.

#### Why does it keep saying "Joining room..." or "Loading camera..."?

If you are accessing the app through a host different from `localhost` then you need to enable `HTTPS`.

At least in Google Chrome, this is because: *Any website which has integrated geolocation technology, screen-sharing, WebRTC and more, will now be required
 to be served from a secure (HTTPS) site.*

You could use [ngrok](https://ngrok.com/) to make an SSL tunnel to your computer. Or you could create a self-signed certificate,
but don't use it in production.

Create an SSL key:

- `[SSL_KEY_PATH]`: your SSL key path
- `[SSL_CERT_PATH]`: your SSL cert path

```bash
$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout "[SSL_KEY_PATH]" -out "[SSL_CERT_PATH]"
```

To enable HTTPS just run `angular-cli` with this command:

```bash
$ ng serve --ssl true --ssl-key "[SSL_KEY_PATH]" --ssl-cert "[SSL_CERT_PATH]" --host=0.0.0.0
```

Since you are not using `localhost`, you need `host=0.0.0.0` to listen for all IPs; you can change it to listen only for the IPs needed.

#### Got more questions?

Open an issue on the AngularOpenVidu [issue tracker][issues].

### License

Apache Software License 2.0 ©

[openvidu-server]: https://github.com/OpenVidu/openvidu/tree/master/openvidu-server

[angular-openvidu-demo]: https://github.com/alxhotel/angular-openvidu-demo

[issues]: https://github.com/alxhotel/angular-openvidu/issues

[travis-image]: https://img.shields.io/travis/alxhotel/angular-openvidu/master.svg
[travis-url]: https://travis-ci.org/alxhotel/angular-openvidu
[dependency-status-image]: https://david-dm.org/alxhotel/angular-openvidu.svg
[dependency-status-url]: https://david-dm.org/alxhotel/angular-openvidu
[codelyzer-image]: https://img.shields.io/badge/code_style-codelyzer-brightgreen.svg
[codelyzer-url]: https://github.com/mgechev/codelyzer
[license-image]: https://img.shields.io/badge/License-Apache%202.0-blue.svg
[license-url]: https://raw.githubusercontent.com/alxhotel/angular-openvidu/master/LICENSE
