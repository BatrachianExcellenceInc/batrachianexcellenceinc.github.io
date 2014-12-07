---
layout: post
title: Running the TextSecure server
author: mjtorn
tags:
  - TextSecure
  - TextSecure Server
---

As an Acolyte Junior I was tasked with setting up [TextSecure server](https://github.com/WhisperSystems/TextSecure-Server/) for the development of our in-house client library.

You may want to check [the official documentation](https://github.com/WhisperSystems/TextSecure-Server/wiki/Using-your-own-server), especially issue 5 which is linked at the top. For developing a websocket client most of it is not relevant. This is.

At the time of writing this, the following seem superfluous:

  * APN and GCM - We're doing websockets
  * S3 - We can figure that out later, or enable it later
  * Twilio - We can ask PostgreSQL about pending accounts

Fortunately these can all be disabled easily in the code. APN and GCM need to not be started. The configuration parser can be tweaked to allow more nulls.

I have posted [a code diff with an example configuration](https://gist.github.com/mjtorn/e57db1dfa0fed9e7c790) on Github. It should apply cleanly enough even in the future, but in case it does not it will give you a clue.

After that it's all straightforward:

    $ mvn package
    $ java -jar target/TextSecureServer-0.22.jar db migrate local.yml
    $ java -jar target/TextSecureServer-0.22.jar server local.yml

Now it is possible to make HTTP requests for new verification codes against ``http://localhost:8080/``. It is also possible to query the database for pending accounts.

This phase of the work is done. There is more to do later.

The tadpoles are about to hatch.

