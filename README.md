# Vite-Installation-Laravel-For-JQuery-Bootstrap-Admin-Framework

**Remove MIX and Install Vite**

Step 1. Remove mix(webpack.mix.js) from root folder by running below command

		    npm remove laravel-mix

Step 2. Install Vite by running below command, Once installed, it will generate a vite.config.js file in the root of the project folder.

		    npm install --save-dev vite laravel-vite-plugin

Step 3. Update NPM **script** in package.json, just keep below 2 values
	   	"dev": "vite",
		"build": "vite build"

Step 4. In resources/js/app.js
		Replace "require('./bootstrap');" with "import './bootstrap';"

Step 5. In resources/js/bootstrap.js

		window._ = require('lodash'); **Replace with** import _ from 'lodash'; window._ = _;
		
		window.axios = require('axios'); **Replace with** import axios from 'axios'; window.axios = axios;

		window.Pusher = require('pusher-js'); **Repalce with** import Pusher from 'pusher-js'; window.Pusher = Pusher; 

Step 6. Remove mix keys and add Vite in env file

		MIX_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
 		MIX_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"

 		Replace with
 		
		VITE_PUSHER_APP_KEY="${PUSHER_APP_KEY}"	
		VITE_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"
		

Step 7. In resources\js\bootstrap.js

		key: process.env.MIX_PUSHER_APP_KEY,
		cluster: process.env.MIX_PUSHER_APP_CLUSTER,
		
		Replace with
		
		key: import.meta.env.VITE_PUSHER_APP_KEY,
		cluster: import.meta.env.VITE_PUSHER_APP_CLUSTER,

**Install Jquery and import css and js file using Vite**

Step 1. Install Jquery

		    npm install jquery
	
Step 2. include below statement in resources/js/app.js

			import $ from 'jquery';
		    window.$ = window.jQuery = $;
	
Step 3. Configure CSS and JS files of custom admin layout in vite.config.js
	
	      	import { defineConfig } from 'vite';
	      	import laravel from 'laravel-vite-plugin';
	 
	      	export default defineConfig({
	      		plugins: [
	      			laravel({
	      					input: [
	      					'resources/css/app.css',
	      					'resources/assets/backend/plugins/fontawesome-free/css/all.min.css',
	      					'resources/assets/backend/plugins/overlayScrollbars/css/OverlayScrollbars.min.css',
	      					'resources/assets/backend/dist/css/adminlte.min.css',
	      					'resources/js/app.js',
	      					'resources/assets/backend/plugins/bootstrap/js/bootstrap.bundle.min.js',
	      					'resources/assets/backend/plugins/overlayScrollbars/js/jquery.overlayScrollbars.min.js',
	      					'resources/assets/backend/dist/js/adminlte.js'
	      				],
	      				refresh:true
	      			}),
	      		]
	      	});

Step 4. Include css and JS files in Blade template 
	
      	- Firstly include css files
      		@vite([
      			'resources/css/app.css',
      			'resources/assets/backend/plugins/fontawesome-free/css/all.min.css',
      			'resources/assets/backend/plugins/overlayScrollbars/css/OverlayScrollbars.min.css',
      			'resources/assets/backend/dist/css/adminlte.min.css',
      			'resources/js/app.js'
      		]);
      	  
      	- Include JS files just before the end of body tag OR in head tag after css files
      		@vite([
      		  'resources/assets/backend/plugins/bootstrap/js/bootstrap.bundle.min.js',
      		  'resources/assets/backend/plugins/overlayScrollbars/js/jquery.overlayScrollbars.min.js',
      		  'resources/assets/backend/dist/js/adminlte.js'
      		]);
	
Step 5. If you run "npm run dev", it will work fine but for "npm run build" you might get "require is not defined" error. 
		    To resolve this error install below package and make some changes in vite.config.js.
		
    		-> npm install vite-plugin-commonjs
    		-> Import package in vite.config.js file
    			import commonjs from 'vite-plugin-commonjs';
    			
    		-> Add "commonjs()" in above plugin object defined in vite.config.js in Step 3

        vite-plugin-commonjs - This package support the libraries that haven’t migrated to ES modules.
