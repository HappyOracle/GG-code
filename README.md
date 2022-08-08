# GG-code

from telethon import TelegramClient
from array import *
from telethon.tl.functions.channels import GetFullChannelRequest
import asyncio
from telethon import TelegramClient, sync, events
from telethon import TelegramClient, events



api_id = 123
api_hash = '123'
client = TelegramClient('anon', api_id, api_hash)
chat = ''
#print(api_id, ) # типа сперва появляется ID и никнейм, а после perepiska
client.start()


@client.on(events.NewMessage(chats=(123)))
async def main(event):
    f = open("telethon.txt", "a+", encoding='utf-16' '\n') #encoding='utf-8' или 'utf-16' - это байт - '\n'
    async for message in client.iter_messages(123):
        from_user = await client.get_entity(message.from_id.user_id)
        print(from_user.username)
        print(message.id, message.text) #bio \n'
        #mess_date = event.newmessage.to_dict()['date'] #ЫЫЫЫ ЕСЛИ ЧЕ УДАЛИ
        #print(client.get_entity(123).stringify()) #фигово работает
        #chat = await client.get_entity(message.chat_id)  # Получаем чат по ИД
        #print(chat.username)
        async for dialog in client.iter_dialogs(): #работает, но фигово
            entity = await client.get_entity(123)
            print(dialog.name, dialog.id)
        async for user in client.iter_participants(chat, filter=123):  # dont work
            print(user.id)
        msg_text = "{User}: {dialog} {id} {Message}  \n".format(User=message.id, dialog=dialog.id, id=user.id, Message=message.text) #user.id mess_date=mess_date,
        f.write(msg_text)
        #dialogs = await client.get_dialogs() #pizda
        #print(dialogs) #gg
        #async for user in client.iter_participants(chat, filter=123):  # dont work
        #    print(user.id)
        #entity = await client.get_entity(123) #работает, но фигово
        #print(entity)
        if message.photo:
            print('File Name :' + str(message.file.name))
            path = await client.download_media(message.media) #message.media, "youranypathher"
            print('File saved to', path)  # printed after download is done
        if message.file:
            print('File Name :' + str(message.file.name))
            path = await client.download_media(message.media) #message.media, "youranypathher"
            print('File saved to', path)  # printed after download is done
with client:
    #messages = client.get_messages(chat, limit=50)
    #print(messages)
    #messages = client.iter_messages('me')
    #f = open("telethon.txt", "a+")
    #for i in range(2):
    #   f.write("Test telethon %d\r\n" % (i + 1)) #создаю тхт файл.

    #f.close()
    client.loop.run_until_complete(main(events))
