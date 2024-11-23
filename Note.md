# Step 1: Create New Laravel Project
>> composer create-project laravel/laravel Laravel_InertiaJs_VueJs


# Step 2: How To Install Vue 3 on Laravel 
>> npm install
>> npm install vue@latest


# Step 3: Install Plugin Vue From Vite
>> npm i @vitejs/plugin-vue



================( Server-Side)==================
# Step 4: Install dependencies For Inertial Js
>> composer require inertiajs/inertia-laravel


# Step 5: Root template setup
"""
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
    @vite('resources/js/app.js')
    @inertiaHead
  </head>
  <body>
    @inertia
  </body>
</html>
"""


# Step 6: Accomplish this by publishing the HandleInertiaRequests middleware
>> php artisan inertia:middleware



# Step 7: HandleInertiaRequests middleware has been published bootstrap/app.php
"""
use App\Http\Middleware\HandleInertiaRequests;

->withMiddleware(function (Middleware $middleware) {
    $middleware->web(append: [
        HandleInertiaRequests::class,
    ]);
})
"""


# Step 8: Creating responses
"""
use Inertia\Inertia;

class EventsController extends Controller
{
    public function show(Event $event)
    {
        return Inertia::render('Event/Show', [
            'event' => $event->only(
                'id',
                'title',
                'start_date',
                'description'
            ),
        ]);
    }
}
"""
================================================



================( Client-Side)==================
# Step 9: Install dependencies
>> npm install @inertiajs/vue3


# Step 10: Initialize the Inertia app in (app.js)
"""
import { createApp, h } from 'vue'
import { createInertiaApp } from '@inertiajs/vue3'

createInertiaApp({
  resolve: name => {
    const pages = import.meta.glob('./Pages/**/*.vue', { eager: true })
    return pages[`./Pages/${name}.vue`]
  },
  setup({ el, App, props, plugin }) {
    createApp({ render: () => h(App, props) })
      .use(plugin)
      .mount(el)
  },
})
"""

Note: Create a `Pages` folder under resources\js this directory

================================================



# Step 11: Install Vitejs
>> npm i @vitejs/plugin-vue


# Step 12: vue add in vite.config.js file
"""
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';

import vue from '@vitejs/plugin-vue'

export default defineConfig({
    plugins: [
        vue(),
        
        laravel({
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
    ],
});

"""
