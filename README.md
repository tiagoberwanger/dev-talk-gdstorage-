# DEV TALK GDSTORAGE

### PRE-REQUISITOS:

Criar um Google Project no GOOGLE CLOUD PLATFORM, ativar a API e copiar a chave JSON com os detalhes desse projeto.


## PASSOS:

### PASSO 1 - Instalar a dependência

```pip install django-googledrive-storage```

### PASSO 2 - Adicionar nos INSTALLED_APPS

```INSTALLED_APPS = (
    ...,
    'django.contrib.staticfiles',
    'gdstorage'
)
```

### PASSO 3 - No settings.py adicionar os caminhos para a chave JSON do Google Project

```GOOGLE_DRIVE_STORAGE_JSON_KEY_FILE = '<path to your json private key file>'```
```GOOGLE_DRIVE_STORAGE_MEDIA_ROOT = '<base google drive path for file uploads>'```


### PASSO 4 - No models.py instanciar o GDSTORAGE

```gd_storage = GoogleDriveStorage()```

### PASSO 5 - No model criado para o upload adicionar o campo storage apontando para a instância do GDSTORAGE

````
class File(models.Model):
    id = models.AutoField( primary_key=True)
    file_name = models.CharField(max_length=200)
    file_data = models.FileField(upload_to='path', storage=gd_storage)
```

### PASSO 6 (opcional) - Definir permissões

```
from gdstorage.storage import GoogleDriveStorage, GoogleDrivePermissionType, GoogleDrivePermissionRole, GoogleDriveFilePermission

permission =  GoogleDriveFilePermission(
   GoogleDrivePermissionRole.READER,
   GoogleDrivePermissionType.USER,
   "email@email.com"
)

gd_storage = GoogleDriveStorage(permissions=(permission, ))

class File(models.Model):
    id = models.AutoField( primary_key=True)
    file_name = models.CharField(max_length=200)
    file_data = models.FileField(upload_to='path', storage=gd_storage)
```

### ENJOY
