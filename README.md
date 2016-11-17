erxes is an open-source messaging platform for customer success.

# Developer install guide

## Install meteor

```bash
curl https://install.meteor.com/ | sh
```

We need to run three apps (main meteor and 2 simple static file server) in order to
simulate real life environment.

## Setup main app

Clone repo

```bash
git clone https://github.com/erxes/erxes.git
cd erxes
```

Install dependencies in main app

```bash
cd main
meteor npm install
```

Create settings file

```bash
cp settings.json.example settings.json
```

Configure settings. Open settings.json and edit it.

```bash
{
  "public": {
    # your erxes deployed domain
    "CDN_HOST": "http://127.0.0.1/static"
  },

  "COMPANY_NAME": "{your_company_name}",
  "NO_REPLY_EMAIL": "{no-reply@{domain}}",

  # amazon s3 credientials. Using to upload attachents, profile pictures etc ...
  "AWS_accessKeyId": "{access_key_id}",
  "AWS_secretAccessKey": "{secret_access_key}",
  "AWS_bucket": "{bucket_name}",
}
```

Run

```bash
./start.sh
```

Now, main app is running at <a href="localhost:7010" target="__blank">http://localhost:7010</a>.
Default channel, brand, integration must be created. Login using
```bash
email: 'admin@erxes.io'
password: 'admin123'
```

## Setup api app

Install dependencies

```bash
cd ../api
meteor npm install
```

Create settings file

```bash
cp settings.json.example settings.json
```

Configure settings. Open settings.json and edit it.

```bash
{
  # your erxes deployed domain
  "CDN_HOST": "http://127.0.0.1:7020/static",
  "API_URL": "ws://127.0.0.1:7010/websocket"
}
```

Run

```bash
./start.sh
```

> If you face with `gulp command not found` error, install it by `npm install -g gulp`
command.

Api app is running at <a href="http://localhost:7020" target="__blank">http://localhost:7020</a>.

## Setup publisher app

```bash
cd ../publisher
./start.sh
```

Publisher app is running at <a href="http://localhost:7030" target="__blank">http://localhost:7030</a>.

Now, everything is set. You can play around with the widget in the publisher app.
Send message from publisher and respond from main app.

## Run test

```bash
cd ../main
meteor npm test
```