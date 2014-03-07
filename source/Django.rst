Django
======


=======================================================
Как добавить пустой выбор в СhoiceField для ModelForm?
=======================================================

::

	from django.db import models

	class Project(models.Model):
	    name = models.CharField(max_length=140)
	    parent = models.ForeignKey('self', blank=True, null=True)

	class ProjectForm(ModelForm):
	    def __init__(self, *args, **kwargs):
	        super(ProjectForm, self).__init__(*args, **kwargs)
	        ordered = []
	        // ... making ordered list ...
	        self.fields['parent'].choices = ordered
        self.fields['parent'].choices.insert(0, ('', u'------'))



=============================================
Deserialize request
=============================================

::

	data = self.deserialize(
	            request,
	            request.raw_post_data,
	            format=request.META.get('CONTENT_TYPE', 'application/json'))


===================================================
Как объединить querysets от одной и той же модели?
===================================================

::

	from itertools import chain
	result_list = list(chain(page_list, article_list, post_list))


=============================================
Автозаполнение даты в модели
=============================================

::

	import datetime
	from django.db import models

	class News(models.Model):
	    pub_date = models.DateTimeField(u'Дата публикации', blank=False, default=datetime.datetime.now)


=============================================
Ошибка с native DateTimeField
=============================================

Ошибка: ::

	remote: /usr/local/lib/python2.7/dist-packages/django/db/models/fields/__init__.py:808: 
		RuntimeWarning: DateTimeField received a naive datetime (2012-08-14 10:18:39.892967) 
		while time zone support is active.
	remote:   RuntimeWarning)

Возникает при заполнении базы по команде ``python manage.py migrate``.

Решение: ::

	from django.utils.timezone  import utc
	datetime=datetime.datetime.utcnow().replace(tzinfo = utc)


=============================================
How to set a label for a field that is a method
=============================================

::

	class MyAdmin(...):
		list_display = ('_my_field',)

		def _my_field(self, obj):
			return obj.get_full_name()
		_my_field.short_description = 'my custom label'



=============================================
Расширение shell_plus
=============================================

Откуда берется: https://github.com/django-extensions/django-extensions

Как запустить: ``python manage.py shell_plus``

Чтобы shell_plus перезапускался каждый раз когда что-то меняется в коде на django:

::

	%load_ext autoreload
	%autoreload 2

Как написать макрос для повторяющихся действий:

::

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


=============================================
translation
=============================================

::

	for d in app catalog common community contact event festival userprofile; do
	cd $d
	../manage.py makemessages --all
	cd ..
	done
