## Getting Around Same Origin Policy

- So, we basically need a way around Same Origin Policy to allow two different origins to communicate
- We will start with URL fragment and try using its behaviour and try to talk cross origin
  - Its been very old loophole in Same Origin Policy
  - We know that parent is allowed to navigate child frames



**postMessage**

- We use postMessage API only when both sides are ready to cooperate into doing some community or sharing data.
-  