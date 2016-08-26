# Django

## Forms

### Emty choice

```python
from django.db.models.fields import BLANK_CHOICE_DASH
```

### How to set a label for a field that is a method

	class MyAdmin(...):
		list_display = ('_my_field',)

		def _my_field(self, obj):
			return obj.get_full_name()
		_my_field.short_description = 'my custom label'


### iPython

	%load_ext autoreload
	%autoreload 2

### Как написать макрос для повторяющихся действий:

	In [8]: print 1
	1
	In [9]: print 2
	2
	In [10]: print 34
	34

	In [12]: macro cosa 8 9 10
	Macro `cosa` created. To execute, type its name (without quotes).
	=== Macro contents: ===
	print 1
	print 2
	print 34

	In [13]: cosa
	1
	2
	34

	In [14]: %edit cosa


### translation

    for d in app catalog common community contact event festival userprofile; do
    cd $d
    ../manage.py makemessages --all
    cd ..
    done
