# Telegram log target for Yii 2

[Telegram](https://telegram.org) log target for Yii 2.

Fork from [sergeymakinen/yii2-telegram-log](https://github.com/sergeymakinen/yii2-telegram-log)

## Installation

The preferred way to install this extension is through [composer](https://getcomposer.org/download/).

Either run

```bash
composer require "spayn/yii2-log-telegram"
```

## Usage

First [create a new bot](https://core.telegram.org/bots#6-botfather) and obtain its token. It should look like `123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11`.

You will also need a [chat ID](https://stackoverflow.com/questions/31078710/how-to-obtain-telegram-chat-id-for-a-specific-user) to send logs to. You can use the [`@get_id_bot`](https://telegram.me/get_id_bot) bot to obtain it. It should look like `123456789`.

Then set the following Yii 2 configuration parameters:

```php
'components' => [
    'log' => [
        'targets' => [
            [
                'class' => 'sergeymakinen\yii\telegramlog\Target',
                'token' => '123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11',
                'chatId' => 123456789,
            ],
        ],
    ],
],
```

## Configuration

By default `yii\log\Logger` error levels are mapped to emojis (you can tweak them in the `levelEmojis` property):

| Error level | Emoji
| --- | ---
`Logger::LEVEL_ERROR` | ☠️
`Logger::LEVEL_WARNING` | ⚠️
`Logger::LEVEL_INFO` | ℹ️
`Logger::LEVEL_TRACE` | 📝

It's also possible to disable notifications - entirely or per logger level (look at the `enableNotification` property), for example:

```php
public $enableNotification = [
    Logger::LEVEL_ERROR => true,
    Logger::LEVEL_WARNING => false,
    Logger::LEVEL_INFO => false,
];
```

This will disable notifications for warning and info level messages and enable them for other levels (honestly, you can omit the `LEVEL_ERROR` definition here as it's `true` by default).
