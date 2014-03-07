Javascript
=======

===========================================================================
How to det window location without hash and get parameters?
===========================================================================

::

    window.location.href.split('#')[0].split('?')[0]


===========================================================================
ExtJS: Как получить полный url для grid, по которому он ходит при загрузки store?
===========================================================================

::

	grid = Ext.getCmp('MyGrid');
	var url = grid.getStore().getProxy().api.read;
	var params = grid.getStore().getProxy().extraParams;
	params['new_param'] = 'value';
	var newUrl = url + '?' + Ext.Object.toQueryString (params);
	window.open(newUrl,'_blank');


.. _источник: http://stackoverflow.com/questions/12561915/extjs-4-how-can-i-get-the-complete-url-with-params-from-a-currently-loaded-gri
`источник`_

