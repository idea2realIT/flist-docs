---
sidebar_position: 1
---

# Libraries used

## @formatjs/intl-localematcher

### How it works

It exports a named function called match

```js
import { match } from "@formatjs/intl-localematcher";
```

match function takes three aruguments first one is the list of languages that the user-agent is requesting
second one is the list of languages supported by the application and the third one is the fallback language.

```ts
function formatHeaders(request: NextRequest) {
  const headers: { [key: string]: string } = {};
  request.headers.forEach((value, key) => (headers[key] = value));
  return headers;
}

export default function LanguageMiddleware(request: NextRequest) {
  const headers = formatHeaders(request);
  const negotiator = new Negotiator({ ...request, headers: headers });
  let locales = ["en", "en-US", "nl-NL", "nl"];
  console.log("languages requested", negotiator.languages());
  const matched = match(negotiator.languages(), locales, "en");
  console.log("matched languages", matched);
}
```

be carefull in choosing locales order because it will affect how the `match` function match the language

you can learn about the working algorithm of the above function [here](https://github.com/tc39/proposal-intl-localematcher)
