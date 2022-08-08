# GG-code

Прочее

from telethon import TelegramClient, events
client = TelegramClient('anon', api_id=17876697, api_hash='f57224fa791de500d30a17a4fbb650ec')
client.start()

@client.on(events.NewMessage(chats=('python_scripts')))
async def normal_hardler(event):
    mess_date = event.message.to_dict()['date']
    mess_id = event.message.to_dict()['id']
    print(event.message.to_dict()['message'])
    print(mess_date,mess_id)
    print('--------------------------')

client.run_until_disconnected()




#@client.on(events.NewMessage(outgoing=True, pattern=r'\.save'))
#async def handler(event):
#    if event.is_reply:
#        replied = await event.get_reply_message()
#        sender = replied.sender
#        await client.download_profile_photo(sender)
#        await event.respond('Saved your photo {}'.format(sender.username)) #'Saved your photo {}'
