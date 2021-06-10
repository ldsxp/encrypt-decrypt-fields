# Django Encrypt Decrypt
 
A Django model field that encrypt your data based SHA256 algorithm on  when save to model field. It keeps data always encrypted in database.

## Usage


Use project secret key or own:

```
from django.conf import settings
from django.db import Model
from django_encrypt_decrypt import EncryptedTextField


class DemoModel(models.Models):
    password = EncryptedTextField(blank=True, key=settings.SECRET_KEY)
```

```
DemoModel.objects.create(password='password')
```

```
obj = DemoModel.objects.get(id=1)
obj.password  # 'bYijegsEDrmS1s7iuytt5TUgglnspA'
```

To decrypt value use Crypto class:

```
from django.conf import settings
from django_encrypt_decrypt import Crypto

obj = DemoModel.objects.get(id=1)

decrypted = Crypto(settings.SECRET_KEY).decrypt_token(obj.password)
decrypted  # 'password'
```