# node-jawbone-up

Jawbone UP API Node.js Library

API Version: v.1.1

If you would like to contribute to this project in any way, including to update it to support API v1.1, please send me a pull request!

Official UP API: [jawbone.com/up/developer](https://jawbone.com/up/developer/)

[![Build Status](https://secure.travis-ci.org/ryanseys/node-jawbone-up.png)](http://travis-ci.org/ryanseys/node-jawbone-up)

[![NPM](https://nodei.co/npm/jawbone-up.png)](https://npmjs.org/package/jawbone-up)

## Installation

`npm install jawbone-up`

## Usage

An `access_token` attribute is required in the options object!
See below for an example of how this could be done. This library does not
assist in getting an `access_token` through OAuth, but once you get the token,
it will apparently last for a **year**.

```javascript
var options = {
  // ** REQUIRED **
  access_token:  'xyz'  // Access token for specific user,
  client_secret: 'abc'  // Client Secret (required for up.refreshToken.get())
}

var up = require('jawbone-up')(options);
```

# Documentation

Official UP API can be found at [jawbone.com/up/developer](https://jawbone.com/up/developer/)

Generated documentation for this library is hosted at [ryanseys.github.io/node-jawbone-up/docs](http://ryanseys.github.io/node-jawbone-up/docs/)

You can also generate the docs yourself:

```
npm install
node_modules/.bin/jsdoc . -d docs
```

Or see below for an overview...

The callback function will follow the format as specified below:

```javascript
function callback(err, body) {
  // do stuff
}
```

Example callback:

```javascript
// Callback function returns an error if applicable
// and/or the body of the API response
function callback(err, body) {
  if(err) {
    console.log('Error: ' + err);
  }
  else {
    var data = JSON.parse(body).data;
    // do something with data
  }
}
```

## User information

```javascript
// get user info
up.me.get({}, callback)             // GET /nudge/api/v.1.1/users/@me/

// get friends of user
up.friends.get({}, callback)        // GET /nudge/api/v.1.1/users/@me/friends

// get mood of user
up.mood.get({}, callback)           // GET /nudge/api/v.1.1/users/@me/mood

// get trends of user
up.trends.get({}, callback)         // GET /nudge/api/v.1.1/users/@me/trends

// get goals of user
up.goals.get({}, callback)          // GET /nudge/api/v.1.1/users/@me/goals
```

## Moves

```javascript
// get all moves (paginated results)
up.moves.get({}, callback)                      // GET /nudge/api/v.1.1/users/@me/moves

// get a specific moves
up.moves.get({ xid : move_xid }, callback)      // GET /nudge/api/v.1.1/moves/{move_xid}

// get a specific move image
up.moves.image({ xid : move_xid }, callback)    // GET /nudge/api/v.1.1/moves/{move_xid}/image

// get a specific move intensity
up.moves.ticks({ xid : move_xid }, callback) // GET /nudge/api/v.1.1/moves/{move_xid}/ticks
```

## Workouts

```javascript
// get all workouts (paginated results)
up.workouts.get({}, callback)                         // GET /nudge/api/v.1.1/users/@me/workouts

// create a new workout
up.workouts.create(options, callback)                 // POST /nudge/api/v.1.1/users/@me/workouts

// get a specific workout
up.workouts.get({ xid : workout_xid }, callback)      // GET /nudge/api/v.1.1/workouts/{workout_xid}

// update a specific workout
up.workouts.update(options, callback)                 // POST https://jawbone.com/nudge/api/v.1.1/workouts/{xid}/partialUpdate

// get a specific workout image
up.workouts.image({ xid : workout_xid }, callback)    // GET /nudge/api/v.1.1/workouts/{workout_xid}/image

// get a specific workout intensity
up.workouts.ticks({ xid : workout_xid }, callback) // GET /nudge/api/v.1.1/workouts/{workout_xid}/ticks
```

## Sleeps

```javascript
// get all sleeps (paginated results)
up.sleeps.get({}, callback)                           // GET /nudge/api/v.1.1/users/@me/sleeps

// get a specific sleep
up.sleeps.get({ xid : sleep_xid }, callback)          // GET /nudge/api/v.1.1/sleeps/{sleep_xid}

// create a new sleep
up.sleeps.create(options, callback)                   // POST /nudge/api/v.1.1/users/@me/sleeps

// get a specific sleep image
up.sleeps.image({ xid : sleep_xid }, callback)        // GET /nudge/api/v.1.1/sleeps/{sleep_xid}/image

// get a specific sleep ticks
up.sleeps.ticks({ xid : sleep_xid }, callback)     // GET /nudge/api/v.1.1/sleeps/{sleep_xid}/ticks

// delete a specific sleep
up.sleeps.delete({ xid : sleep_xid }, callback)       // DELETE /nudge/api/v.1.1/sleeps/{sleep_xid}
```

## Meals

```javascript
// get all meals (paginated results)
up.meals.get({}, callback)                   // GET /nudge/api/v.1.1/users/@me/meals

// create a new meal
up.meals.create(options, callback)           // POST /nudge/api/v.1.1/users/@me/meals

// update a specific meal
up.meals.update(options, callback)           // POST https://jawbone.com/nudge/api/v.1.1/meals/{xid}/partialUpdate

// get a specific meal
up.meals.get({ xid : meal_xid }, callback)   // GET /nudge/api/v.1.1/meals/{meal_xid}
```

## Body Composition

```javascript
// get all body events (paginated results)
up.events.body.get({}, callback)                      // GET /nudge/api/v.1.1/users/@me/body_events

// get a specific body event
up.events.body.get({ xid : event_xid }, callback)     // GET /nudge/api/v.1.1/body_events/{event_xid}

// create a new body event
up.events.body.create(options, callback)              // POST /nudge/api/v.1.1/users/@me/body_events

// delete a specific body event
up.events.body.delete({ xid : event_xid }, callback)  // DELETE /nudge/api/v.1.1/body_events/{event_xid}
```

## Cardiac Metrics

```javascript
// get all cardiac events (paginated results)
up.events.cardiac.get({}, callback)                      // GET /nudge/api/v.1.1/users/@me/cardiac_events

// get a specific cardiac event
up.events.cardiac.get({ xid : event_xid }, callback)     // GET /nudge/api/v.1.1/cardiac_events/{event_xid}

// create a new cardiac event
up.events.cardiac.create(options, callback)              // POST /nudge/api/v.1.1/users/@me/cardiac_events

// delete a specific cardiac event
up.events.cardiac.delete({ xid : event_xid }, callback)  // DELETE /nudge/api/v.1.1/cardiac_events/{event_xid}
```

## Generic Events

```javascript
// get all generic events (paginated results)
up.events.generic.get({}, callback)                      // GET /nudge/api/v.1.1/users/@me/generic_events

// get a specific generic event
up.events.generic.get({ xid : event_xid }, callback)     // GET /nudge/api/v.1.1/generic_events/{event_xid}

// create a new generic event
up.events.generic.create(options, callback)              // POST /nudge/api/v.1.1/users/@me/generic_events

// update an existing generic event
up.events.generic.update(options, callback)              // POST /nudge/api/v.1.1/users/@me/generic_events/{xid}/partialUpdate

// delete a specific generic event
up.events.generic.delete({ xid : event_xid }, callback)  // DELETE /nudge/api/v.1.1/generic_events/{event_xid}
```

## Mood

```javascript
// get all moods (paginated results)
up.mood.get({}, callback)                     // GET /nudge/api/v.1.1/users/@me/mood

// get a specific mood
up.mood.get({ xid : mood_xid }, callback)     // GET /nudge/api/v.1.1/mood/{mood_xid}

// create a new mood
up.mood.create(options, callback)             // POST /nudge/api/v.1.1/users/@me/mood

// delete a specific mood
up.mood.delete({ xid : mood_xid }, callback)  // DELETE /nudge/api/v.1.1/mood/{mood_xid}
```

## Time Zone

```javascript
// get a user's timezone
up.timezone.get({}, callback) // GET /nudge/api/v.1.1/users/@me/timezone
```

## Refresh Token

Added in v.1.1

```javascript
// get (technically POST) a refresh token (requires client_secret passed into options when initializing)
up.refreshToken.get(callback) // POST /nudge/api/v.1.1/users/@me/refreshToken
```

## Settings

Added in v.1.1

```javascript
// get user settings
up.settings.get(callback) // GET /nudge/api/v.1.1/users/@me/settings
```

## Webhook

Added in v.1.1

```javascript
// create a webhook
up.webhook.create(webhook_url, callback) // POST /users/@me/pubsub?webhook={webhook_url};
```

```javascript
// delete a webhook
up.webhook.delete(callback) // DELETE /users/@me/pubsub
```

# Tests

Tests can be found in the `test` folder.

To run tests:

Make sure you first have dependencies installed by running:

```bash
npm install
```

Then you may run all the tests with:

```bash
npm test
```

# Contributing

I would love contributions. Filing issues [on Github](https://github.com/ryanseys/node-jawbone-up/issues)
or sending pull requests is always greatly appreciated.

# License

The MIT License (MIT)

Copyright (c) 2013 Ryan Seys

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

