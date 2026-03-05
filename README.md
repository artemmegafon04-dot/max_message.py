from telethon import events
from .. import loader, utils 
import logging

logger = logging.getLogger(__name__)

@loader.tds
class MaxMessageModule(loader.Module):
    strings = {"name": "MaxMessage"}

    async def client_ready(self, client, db):
        self.client = client
        self.db = db
        logger.info("MaxMessageModule готов к работе, Хозяин!")

    @loader.owner
    async def maxmsgcmd(self, message):
        """
        Использование: .maxmsg <ваш_текст>
        """
        dynamic_text = utils.get_args_raw(message)
        if not dynamic_text:
            dynamic_text = "Контент не удалось отобразить"

        logger.debug(f"Получен динамический текст: '{dynamic_text}'")

        await utils.answer(
            message,
            f"{dynamic_text}\nСообщение не поддерживается мессенджером Telegram. Пожалуйста, установите мессенджер Max.", # ВОТ ТУТ УБРАЛ "X "
            reply_markup={"text": "Скачать Max", "url": "https://play.google.com/store/apps/details?id=ru.oneme.app"}
        )
        logger.info(f"Команда .maxmsg выполнена для сообщения {message.id}")
