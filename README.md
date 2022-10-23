# aiogram_unittest

***aiogram_unittest*** is a testing library for bots written on <a href="https://github.com/aiogram/aiogram">aiogram</a>

## 📚 Simple examples

### Simple handler test

#### Simple bot:

```python
from aiogram import Bot, Dispatcher, types, executor

# Please, keep your bot tokens on environments, this code only example
bot = Bot('123456789:AABBCCDDEEFFaabbccddeeff-1234567890')
dp = Dispatcher(bot)


@dp.message_handler()
async def echo(message: types.Message):
    await message.answer(message.text)


if __name__ == '__main__':
    executor.start_polling(dp)


```

#### Test cases:

```python
import unittest

from aiogram import types
from bot import echo

from aiogram_unittest import Requester, RequestType
from aiogram_unittest.types.dataset import MESSAGE
from aiogram_unittest.handler import MessageHandler


class TestBot(unittest.IsolatedAsyncioTestCase):
    async def test_echo(self):
        request = Requester(request_handler=MessageHandler(echo))

        calls = await request.query(MESSAGE.as_object(text="Hello, Bot!"))

        answer_message = calls.send_messsage.fetchone()
        self.assertEqual(answer_message.text, 'Hello, Bot!')

```

### ▶️ <a href='https://OCCCAS/aiogram_unittest/examples'>More</a> examples

