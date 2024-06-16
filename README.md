# Практична з пайтона на юпітер.
## Ось код: 
```
import ipywidgets as widgets
from IPython.display import display, clear_output

class EncryptionAlgorithm:
    def encrypt(self, text, key):
        raise NotImplementedError("Метод шифрування не реалізовано")

    def decrypt(self, text, key):
        raise NotImplementedError("Метод розшифровки не реалізовано")

class CaesarCipher(EncryptionAlgorithm):
    def encrypt(self, text, key):
        encrypted_text = ''.join(
            chr((ord(char) + key - 65) % 26 + 65) if char.isupper() else
            chr((ord(char) + key - 97) % 26 + 97) if char.islower() else char
            for char in text
        )
        return encrypted_text

    def decrypt(self, text, key):
        return self.encrypt(text, -key)

class XORCipher(EncryptionAlgorithm):
    def encrypt(self, text, key):
        return ''.join(chr(ord(char) ^ key) for char in text)

    def decrypt(self, text, key):
        return self.encrypt(text, key)

algorithm_selector = widgets.Dropdown(
    options=['Caesar-Cipher', 'XOR-Cipher'],
    value='Caesar-Cipher',
)

text_input = widgets.Textarea(
    value='',
    placeholder='',
    description='Текст:',
    layout=widgets.Layout(width='50%', height='100px')
)

key_input = widgets.IntText(
    value=1,
    description='Ключ:',
    layout=widgets.Layout(width='50%')
)

encrypt_button = widgets.Button(description="Зашифрувати")
decrypt_button = widgets.Button(description="Розшифрувати")

output = widgets.Textarea(
    value='',
    placeholder='',
    description='Результат:',
    layout=widgets.Layout(width='50%', height='100px')
)

def on_encrypt_button_clicked(b):
    clear_output()
    display(ui)
    algorithm = algorithm_selector.value
    text = text_input.value
    key = key_input.value
    if algorithm == 'Caesar-Cipher':
        cipher = CaesarCipher()
    elif algorithm == 'XOR-Cipher':
        cipher = XORCipher()
    encrypted_text = cipher.encrypt(text, key)
    output.value = encrypted_text

def on_decrypt_button_clicked(b):
    clear_output()
    display(ui)
    algorithm = algorithm_selector.value
    text = text_input.value
    key = key_input.value
    if algorithm == 'Caesar-Cipher':
        cipher = CaesarCipher()
    elif algorithm == 'XOR-Cipher':
        cipher = XORCipher()
    decrypted_text = cipher.decrypt(text, key)
    output.value = decrypted_text

encrypt_button.on_click(on_encrypt_button_clicked)
decrypt_button.on_click(on_decrypt_button_clicked)

ui = widgets.VBox([
    algorithm_selector,
    text_input,
    key_input,
    encrypt_button,
    decrypt_button,
    output
])

display(ui)
```
## Скріни в репозиторію
