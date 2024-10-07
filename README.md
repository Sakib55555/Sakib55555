from telegram.ext import Updater, CommandHandler
from telegram import ParseMode

# বট টোকেন ব্যবহার করে আপডেটার তৈরি
API_TOKEN = 'আপনার_বট_টোকেন_এখানে'

# রেফারেল ডাটাবেস (এটি সাধারণ উদাহরণ)
referral_data = {}

def start(update, context):
    # ব্যবহারকারীকে স্বাগতম বার্তা পাঠানো
    user = update.message.from_user
    user_id = user.id
    referral_code = str(user_id)

    welcome_text = f"হ্যালো {user.first_name}!\n\n"
    welcome_text += f"আপনার রেফারেল কোড: `{referral_code}`\n"
    welcome_text += "এই কোডটি শেয়ার করুন এবং বন্ধুদের আমন্ত্রণ জানান!"

    update.message.reply_text(welcome_text, parse_mode=ParseMode.MARKDOWN)

def refer(update, context):
    # রেফারেল কোডের মাধ্যমে আমন্ত্রিত ব্যবহারকারী সনাক্ত করা
    user = update.message.from_user
    if len(context.args) > 0:
        referral_code = context.args[0]
        referred_user = user.first_name

        if referral_code in referral_data:
            referrer = referral_data[referral_code]
            referrer['referrals'] += 1

            message = f"ধন্যবাদ {referred_user}!\n"
            message += f"{referrer['name']} কে রেফার করার জন্য।\n"
            message += f"{referrer['name']} এখন পর্যন্ত {referrer['referrals']} জনকে রেফার করেছেন।"
        else:
            message = "অবৈধ রেফারেল কোড।"
    else:
        message = "দয়া করে একটি রেফারেল কোড প্রদান করুন।"

    update.message.reply_text(message)

def main():
    updater = Updater(API_TOKEN, use_context=True)
    dp = updater.dispatcher

    # কমান্ড হ্যান্ডলার
    dp.add_handler(CommandHandler("start", start))
    dp.add_handler(CommandHandler("refer", refer))

    # বট চালু করা
    updater.start_polling()
    updater.idle()

if __name__ == '__main__':
    main()- 👋 Hi, I’m @Sakib55555
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Sakib55555/Sakib55555 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
