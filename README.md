# Django Signals Demo

This repository demonstrates the synchronous execution of Django signals by default.

## Files

- `signals_demo.py`: Contains a Django model and a signal handler to show how signals are executed synchronously.
- `README.md`: Provides an overview of the project and a Q&A section about Django signals.

## Question and Answer

### By default, are Django signals executed synchronously or asynchronously?

**Answer:**
By default, Django signals execute synchronously. This means that when a signal is sent, the connected receivers are executed one by one in the same order in which they were connected, and the signal sender waits for all receivers to finish before continuing execution.

Here’s a code snippet that demonstrates this behavior:

```python
from django.db.models.signals import post_save
from django.dispatch import receiver
from django.db import models

class MyModel(models.Model):
    name = models.CharField(max_length=100)

@receiver(post_save, sender=MyModel)
def my_signal_handler(sender, instance, **kwargs):
    print("Signal received for:", instance.name)

# Creating an instance of MyModel
obj = MyModel.objects.create(name="Test")
print("Object created")  # This will be printed after the signal handler completes

In the above code, we define a Django model MyModel and a signal handler function my_signal_handler that is connected to the post_save signal of MyModel. When an instance of MyModel is created (obj = MyModel.objects.create(name="Test")), the signal is sent and the signal handler is executed synchronously. The print statement "Object created" will only execute after the object has been created and the signal handler has complete
