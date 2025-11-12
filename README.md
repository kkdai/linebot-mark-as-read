LINE Bot Template: A simple Golang LINE Bot for Mark As Read API
==============

 [![GoDoc](https://godoc.org/github.com/kkdai/linebot-mark-as-read.svg?status.svg)](https://godoc.org/github.com/kkdai/linebot-mark-as-read) ![Go](https://github.com/kkdai/linebot-mark-as-read/workflows/Go/badge.svg) [![goreportcard.com](https://goreportcard.com/badge/github.com/kkdai/linebot-mark-as-read)](https://goreportcard.com/report/github.com/kkdai/linebot-mark-as-read)

Installation and Usage
=============

### 1. Got A LINE Bot API devloper account

- [Make sure you already registered on LINE developer console](https://developers.line.biz/console/), if you need use LINE Bot.

- Create new Messaging Channel
- Get `Channel Secret` on "Basic Setting" tab.
- Issue `Channel Access Token` on "Messaging API" tab.
- Open LINE OA manager from "Basic Setting" tab.
- Go to Reply setting on OA manager, enable "webhook"

### 2. Deploy this on Web Platform

You can choose [Heroku](https://www.heroku.com/) or [Render](http://render.com/)

#### 2(A) Deploy this on Heroku

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

- Input `Channel Secret` and `Channel Access Token`.
- Remember your heroku, ID.

#### 2(B) Deploy this on Rener

[![Deploy to Render](http://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy)

### 3. Go to LINE Bot Dashboard, setup basic API

- Setup your basic account information. Here is some info you will need to know.
- `Callback URL`: <https://{YOUR_HEROKU_SERVER_ID}.herokuapp.com/callback>

It all done.

Features
=============

### Mark as Read API

This bot implements LINE's new "Mark as Read" feature, allowing the bot to mark messages as read when users request it.

#### How it works:

1. **User sends a message** (text or sticker)
2. **Bot replies with a Quick Reply button** labeled "Mark as Read"
3. **User clicks the button**
4. **Bot marks the message as read** using the `MarkMessagesAsReadByToken` API
5. **User sees read indicator** in the LINE chat

#### Implementation Details:

- Uses `MarkMessagesAsReadByToken` API from LINE Messaging API v8.18.0
- Extracts `markAsReadToken` from incoming message events (available in `TextMessageContent`, `StickerMessageContent`, etc.)
- Stores the token in Quick Reply button's postback data
- Handles `PostbackEvent` to call the Mark as Read API

#### Code References:

- **Quick Reply Creation**: `main.go:64-75` (Text), `main.go:102-113` (Sticker)
- **Token Extraction**: `main.go:59` (Text), `main.go:97` (Sticker)
- **Postback Handler**: `main.go:142-170`
- **API Call**: `main.go:159-163`

#### Requirements:

- LINE Bot SDK v8.18.0 or higher
- Go 1.24 or higher

#### API Reference:

- **LINE Official Documentation**: [Mark messages as read](https://developers.line.biz/en/reference/messaging-api/#mark-as-read-request-body)
- **SDK Method**: `bot.MarkMessagesAsReadByToken(request)`
- **Request Structure**:
  ```go
  &messaging_api.MarkMessagesAsReadByTokenRequest{
      MarkAsReadToken: markAsReadToken,
  }
  ```

#### Testing:

1. Deploy your bot to Heroku or Render
2. Add the bot as a friend on LINE
3. Send a text message to the bot
4. You'll receive an echo reply with a "Mark as Read" Quick Reply button
5. Click the button
6. Check the bot logs - you should see "Successfully marked messages as read using token"
7. The message will be marked as read in your LINE chat

### Video Tutorial

- [How to deploy LINE BotTemplate](https://www.youtube.com/watch?v=0BIknEz1f8k)
- [Hoe to modify your LINE BotTemplate code](https://www.youtube.com/watch?v=ckij73sIRik)

### Chinese Tutorial

如果你看得懂繁體中文，這裡有[中文的介紹](http://www.evanlin.com/create-your-line-bot-golang/)

Inspired By
=============

- [Golang (heroku) で LINE Bot 作ってみる](http://qiita.com/dongri/items/ba150f04a98e96b160e7)
- [LINE BOT をとりあえずタダで Heroku で動かす](http://qiita.com/yuya_takeyama/items/0660a59d13e2cd0b2516)
- [阿美語萌典 BOT](https://github.com/miaoski/amis-linebot)

Project52
---------------

It is one of my [project 52](https://github.com/kkdai/project52).

License
---------------

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

<http://www.apache.org/licenses/LICENSE-2.0>

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
