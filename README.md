PyRCWS
======

Autorização e captura de transações com webservice da Redecard.


Instalação
----------

    pip install pyrcws

Necessita da lib suds -- é instalada automaticamente com "pip install pyrcws".

Como usar
---------

```python
# coding: utf-8
from decimal import Decimal
from pyrcws import GetAuthorizedException, PaymentAttempt

params = {
    'affiliation_id': '123456789',
    'total': Decimal('0.01'),
    'order_id': '763AH1', # strings are allowed here
    'card_number': '1234567890123456',
    'cvc2': 423,
    'exp_month': 1,
    'exp_year': 2010,
    'card_holders_name': 'JOAO DA SILVA',
    'installments': 1,
}

attempt = PaymentAttempt(**params)
try:
    attempt.get_authorized()
except GetAuthorizedException, e:
    print u'Erro %s: %s' % (e.codret, e.msg)
else:
    attempt.capture()
```

Mais informações
----------------

Os código e a mensagem do erro (GetAuthorizedException) são passados pelo webservice, use o [manual da Redecard](https://services.redecard.com.br/NovoPortal/Portals/_PierNet/documents/Komerci_Manual_Webservice.pdf) disponível no site para mais informações.
