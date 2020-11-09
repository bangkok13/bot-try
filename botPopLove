import telebot
import config
import random

from telebot import types

bot = telebot.TeleBot(config.TOKEN)


@bot.message_handler(commands=['start'])
def welcome(message):
    sti = open('welcome.webp', 'rb')
    bot.send_sticker(message.chat.id, sti)

    # keyboard
    markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
    item1 = types.KeyboardButton("Дезолятор")
    item2 = types.KeyboardButton("Варды")

    markup.add(item1, item2)
    
    bot.send_message(message.chat.id,
                     "Хэй йоу, {0.first_name}!\nЯ - определяю сегдняшние  катки !\nВыбери, что сегодня кпишь!.".format(
                         message.from_user, bot.get_me()),
                     parse_mode='html', reply_markup=markup)



@bot.message_handler(content_types=['text'])
def lalala(message):
    if message.chat.type == 'supergroup':
        if message.text == 'Дезолятор':
            bot.send_message(message.chat.id, "катки-хуятки")
        elif message.text =='Варды':

            markup = types.InlineKeyboardMarkup(row_width=2)
            item1 = types.InlineKeyboardButton("в 19.00", callback_data='good')
            item2 = types.InlineKeyboardButton("в 20.00", callback_data='bad')

            markup.add(item1, item2)

            bot.send_message(message.chat.id, 'Каткам быть!', reply_markup=markup)
        else:
            bot.send_message(message.chat.id, 'БАН, у сука может еще по 500 все купишь?')


@bot.callback_query_handler(func=lambda call: True)
def callback_inline(call):
    try:
        if call.message:
            if call.data == 'good':
                bot.send_message(call.message.chat.id, 'Вот и отличненько')
            elif call.data == 'bad':
                bot.send_sticker(call.message.chat.id, 'CAACAgIAAxkBAAITYV9kVvlMZBxWIyGZmj_ubwy4jSnCAAIbAANlDl0dvow1ZbsCbjcbBA')
                bot.send_message(call.message.chat.id, 'С тебя чипсы клоун') 

           # remove inline buttons
            bot.edit_message_text(chat_id=call.message.chat.id, message_id=call.message.message_id, text="😊",
                                  reply_markup=None)

            # show alert
            bot.answer_callback_query(callback_query_id=call.id, show_alert=False,
                                      text="Найс выбор ебоклак")

    except Exception as e:
        print(repr(e))


# RUN
bot.polling(none_stop=False)
