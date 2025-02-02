# Translator

from tkinter import *
import tkinter as tk
from tkinter import ttk
from googletrans import Translator
from tkinter import messagebox

root = tk.Tk()
root.title('Language Translator')
root.geometry('590x370')

frame1 = Frame(root, width=590, height=370, relief=RIDGE, borderwidth=5, bg='#F7DC6F')
frame1.place(x=0, y=0)

Label(root, text="Language Translator", font=("Helvetica 20 bold"), fg="black", bg='#F7DC6F').pack(pady=10)

language_dict = {
    'Afrikaans': 'af', 'Albanian': 'sq', 'Amharic': 'am', 'Arabic': 'ar',
    'Armenian': 'hy', 'Azerbaijani': 'az', 'Basque': 'eu', 'Belarusian': 'be',
    'Bengali': 'bn', 'Bosnian': 'bs', 'Bulgarian': 'bg', 'Catalan': 'ca',
    'Cebuano': 'ceb', 'Chichewa': 'ny', 'Chinese (Simplified)': 'zh-cn',
    'Chinese (Traditional)': 'zh-tw', 'Corsican': 'co', 'Croatian': 'hr',
    'Czech': 'cs', 'Danish': 'da', 'Dutch': 'nl', 'English': 'en', 'Esperanto': 'eo',
    'Estonian': 'et', 'Filipino': 'tl', 'Finnish': 'fi', 'French': 'fr', 'Frisian': 'fy',
    'Galician': 'gl', 'Georgian': 'ka', 'German': 'de', 'Greek': 'el', 'Gujarati': 'gu',
    'Haitian Creole': 'ht', 'Hausa': 'ha', 'Hawaiian': 'haw', 'Hebrew': 'he',
    'Hindi': 'hi', 'Hmong': 'hmn', 'Hungarian': 'hu', 'Icelandic': 'is', 'Igbo': 'ig',
    'Indonesian': 'id', 'Irish': 'ga', 'Italian': 'it', 'Japanese': 'ja', 'Javanese': 'jv',
    'Kannada': 'kn', 'Kazakh': 'kk', 'Khmer': 'km', 'Kinyarwanda': 'rw', 'Korean': 'ko',
    'Kurdish': 'ku', 'Kyrgyz': 'ky', 'Lao': 'lo', 'Latin': 'la', 'Latvian': 'lv',
    'Lithuanian': 'lt', 'Luxembourgish': 'lb', 'Macedonian': 'mk', 'Malagasy': 'mg',
    'Malay': 'ms', 'Malayalam': 'ml', 'Maltese': 'mt', 'Maori': 'mi', 'Marathi': 'mr',
    'Mongolian': 'mn', 'Nepali': 'ne', 'Norwegian': 'no', 'Odia': 'or', 'Pashto': 'ps',
    'Persian': 'fa', 'Polish': 'pl', 'Portuguese': 'pt', 'Punjabi': 'pa', 'Romanian': 'ro',
    'Russian': 'ru', 'Samoan': 'sm', 'Scots Gaelic': 'gd', 'Serbian': 'sr', 'Sesotho': 'st',
    'Shona': 'sn', 'Sindhi': 'sd', 'Sinhala': 'si', 'Slovak': 'sk', 'Slovenian': 'sl',
    'Somali': 'so', 'Spanish': 'es', 'Sundanese': 'su', 'Swahili': 'sw', 'Swedish': 'sv',
    'Tamil': 'ta', 'Tatar': 'tt', 'Telugu': 'te', 'Thai': 'th', 'Turkish': 'tr',
    'Turkmen': 'tk', 'Ukrainian': 'uk', 'Urdu': 'ur', 'Uzbek': 'uz', 'Vietnamese': 'vi',
    'Welsh': 'cy', 'Xhosa': 'xh', 'Yiddish': 'yi', 'Yoruba': 'yo', 'Zulu': 'zu'
}

def translate():
    lang_1 = text_entry1.get("1.0", "end-1c")
    target_lang = choose_language.get()

    if lang_1 == '':
        messagebox.showerror('Language Translator', 'Enter the text to translate!')
    else:
        text_entry2.delete(1.0, 'end')
        try:
            translator = Translator()
            output = translator.translate(lang_1, dest=language_dict[target_lang])
            if hasattr(output, 'text'):
                text_entry2.insert('end', output.text)
            else:
                messagebox.showerror('Translation Error', 'Translation result could not be obtained.')
        except Exception as e:
            messagebox.showerror('Error', f"An error occurred: {str(e)}")

def clear():
    text_entry1.delete(1.0, 'end')
    text_entry2.delete(1.0, 'end')
    choose_language.current(0)

a = tk.StringVar()

auto_select = ttk.Combobox(frame1, width=27, textvariable=a, state='readonly', font=('verdana', 10, 'bold'))
auto_select['values'] = ('Auto Select')
auto_select.place(x=15, y=60)
auto_select.current(0)

l = tk.StringVar()
choose_language = ttk.Combobox(frame1, width=27, textvariable=l, state='readonly', font=('verdana', 10, 'bold'))
choose_language['values'] = tuple(language_dict.keys())
choose_language.place(x=305, y=60)
choose_language.current(0)

text_entry1 = Text(frame1, width=20, height=7, borderwidth=5, relief=RIDGE, font=('verdana', 15))
text_entry1.place(x=10, y=100)

text_entry2 = Text(frame1, width=20, height=7, borderwidth=5, relief=RIDGE, font=('verdana', 15))
text_entry2.place(x=300, y=100)

btn1 = Button(frame1, command=translate, text='Translate', relief=RAISED, borderwidth=2, font=('verdana', 10, 'bold'), bg='#248aa2', fg='white', cursor='hand2')
btn1.place(x=185, y=300)

btn2 = Button(frame1, command=clear, text='Clear', relief=RAISED, borderwidth=2, font=('verdana', 10, 'bold'), bg='#248aa2', fg='white', cursor='hand2')
btn2.place(x=300, y=300)

root.mainloop()
