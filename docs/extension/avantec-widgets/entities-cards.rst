Entities cards
---------------

Latest values widget.

.. image:: /_static/extension/avantec-widgets/entities-cards-1.png

Configuration:

#. Add all **datasources** and **data keys** in ``Data`` page.
#. Add some **card templates** in ``Advanced`` page. A card template per entity alias used in the datasources.

   * **Alias Name**: Entity alias name.
   * **Card HTML pattern**: HTML template. You can use **${dsName}**, **${entityName}**, **${deviceName}**, **${entityLabel}**, **${aliasName}**, **${entityDescription}**, or *${your_datakey_label}* in it.
   * **Card style function: f(datasource, ctx)**: CSS.

#. Optionally, configure some data keys used in **Card HTML pattern**: ``Data`` page --> Pen icon --> ``Advanced`` page.

   * **Cell content function: f(value, datasource, ctx)**: text or HTML
   * **Cell style function: f(value, datasource, ctx)**: CSS.

#. Add some action in ``Action`` page. A action of element click per entity alias used in the datasources.

   * **Action source**: On HTML element click
   * **Name**: Entity alias name.

#. Optionally, if you want to hide the border of the widget, you should do this in ``Settings`` page:

   * Disable ``Display widget title``.
   * ``Background color`` of the widget should be the same as ``background color`` of Dashboard.

