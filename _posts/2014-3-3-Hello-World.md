---
layout: post
title: PWA Retrospective
---

What worked? What would I do different if I started over?

Vue: Absolutely.

I'm extremely pleased with Vue.

Vuetify: Probably Not.

I don't think I'd use a component library again. It feels like overkill. By using components instead of HTML you are increasing the shadow DOM by a significant amount. Components that render long lists of components, where each list item has more sub components, is sort of a N+1 problem. Now you are rendering 100s or 1000s of components in JS when it all could have been a single component with HTML.

I think a better approach would be to use HTML + CSS framework.



Vuex: Probably Not.

I'd try hard to not use this for storing server side state - ie don't use it as a database. Maybe use IndexDB. I could see using Vuex for pure application state - like have they toggled light or dark mode.



JSON:API: It Depends.  

A large amount of "CRUD" code was written just for the mundane task of converting SQL to JSON on the backend (specifically SQL to JSON:API), then at the client receiving that data, massaging it slightly to store it in Vuex, then later retrieving the data from vuex and converting the data to json again, this time to a proprietary json structure suited to Rails' nested attributes support.

With a solid piece of client-side tooling that takes json:api endpoints and responses, stores those responses , and provides querying that data with support for relationships ... then yes. This is why I spent several weeks trying to use the VuexORM library near the start of the project. But after running into multiple time wasting problems, I gave up and went back to writing my own CRUD everywhere.

Alternatively I'd be tempted to try GraphQL + Apollo and likely a few Apollo extensions/plugins. Maybe Hasura on the backend, if possible.



Netflix / fast_jsonapi (gem): Sure.

If you have to write your own json:api spec API, then fast_jsonapi mostly was excellent. I found some aspects of their API cumbersome, like their use of Proc's for conditionally including attributes.



Axios JS: Yes.


JWT Tokens: I guess.

Simple tokens as credentials is a lovely notion. But it isn't that simple ... there is debate about if those tokens should be stored in localStorage (XSS vulnerable) or cookies (CSRF vulnerable). Then you need the ability to revoke tokens. Lastly you have the matter of refreshing the token. [1]

[1] https://stormpath.com/blog/where-to-store-your-jwts-cookies-vs-html5-web-storage
