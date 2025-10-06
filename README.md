# Vite-Installation-Laravel-For-JQuery-Bootstrap-Admin-Framework

Step 1. Remove mix(webpack.mix.js) from root folder by running below command

		    npm remove laravel-mix

Step 2. Install Vite using running below command, Once installed, it will generate a vite.config.js file in the root of the project folder.

		    npm install --save-dev vite laravel-vite-plugin
	
Step 3. Install Jquery

		    npm install jquery
	
Step 4. include below statement in resources/js/app.js

		    import $ from 'jquery';
		    window.$ = window.jQuery = $;
	
Step 5. Configure CSS and JS files of custom admin layout in vite.config.js
	
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

Step 6. Include css and JS files in Blade template 
	
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
	
Step 7. If you run "npm run dev", it will work fine but for "npm run build" you might get "require is not defined" error. 
		    To resolve this error install below package and make some changes in vite.config.js.
		
    		-> npm install vite-plugin-commonjs
    		-> Import package in vite.config.js file
    			import commonjs from 'vite-plugin-commonjs';
    			
    		-> Add "commonjs()" in above plugin object defined in vite.config.js in Step 3

        vite-plugin-commonjs - This package support the libraries that haven’t migrated to ES modules.
