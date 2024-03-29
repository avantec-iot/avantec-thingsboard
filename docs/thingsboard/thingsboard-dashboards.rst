*******************************
Working with IoT Dashboards
*******************************

Reprinted articles: https://thingsboard.io/docs/user-guide/dashboards/


ThingsBoard allows you to configure customizable IoT dashboards. Each IoT Dashboard may contain multiple dashboard widgets that visualize data from multiple IoT devices. Once IoT Dashboard is created, you may assign it to one of the customers of you IoT project.

IoT Dashboards are light-weight and you may have millions of dashboards. For example, you may automatically create a dashboard for each new customer based on data from registered customer IoT devices. Or you may modify dashboard via script when a new device is assigned to a customer. All these actions may be done manually or automated via REST API.

You can find useful links to get started below:

* `Dashboards`__
    ThingsBoard provides the ability to create and manage dashboards. Each dashboard can contain plenty of widgets. Dashboards display data from many entities: devices, assets, etc. Dashboards can be assigned to Customers.

* `Widgets Library`__
    All IoT Dashboards are constructed using ThingsBoard widgets defined in the Widget Library. Each widget provides end-user functionality such as data visualization, remote device control, alarm management and display of static custom HTML content.

    * **Digital** and **analog** gauges for latest real-time values visualization
    * Highly customizable Bar and Line **charts** for visualization of historical and sliding-window data points
    * **Map** widgets for tracking movement and latest positions of IoT devices on Google or OpenStreet maps.
    * **GPIO** control widgets that allow sending GPIO toggle commands to devices.
    * **Card** widgets to enhance your dashboards with flexible HTML labels based on static content or latest telemetry values from IoT devices.

.. __: https://thingsboard.io/docs/user-guide/ui/dashboards/
.. __: https://thingsboard.io/docs/user-guide/ui/widget-library/

How to customize
=================
* In Avantec Widgets & Avantec Dashboards:
    * Change widget title, background, colors, fonts, shadows, etc
    * Add or remove widget
    * Modify dashboard states, aliases and widget actions
    * Visualizing assets data using Maps and Tables
* Create new Widgets
* Create your Dashboards



Next steps
==================

* ThingsBoard Data visualization
    * `Visualizing assets data using Maps and Tables`__ : Learn how to: create assets and devices and define their relationships; add the server attributes and create a new dashboard; visualize data from the asset attributes using “Entities Table” and “Map” widgets.
    * `Dashboard states, aliases and widget actions`__ : Learn how to: add and configure new dashboard states; create various aliases; visualize the attributes data using the Image Map widget; create actions in different widgets in order to navigate between states; visualize the telemetry data using Analogue and Digital gauges and the Time-series widget.
    * `Remote device control and alarm management`__ : Learn how to: add and use the Knob Control widget; create alarm rules; handle alarms using the Alarms widget; make a dashboard public.
    * `Basic widget settings`__ : Learn how to: change widget title, background, colors, fonts, shadows, etc.
    * `Latest Values Map widget`__ : Learn how to create Map widget, based on latitude and longitude, and customize the Map widget layout and properties.
    * `Time Series Map widget`__ : Learn how to display your devices with the latest telemetry data on the Time Series Map widget and modify the widget properties.
    * `Trip Animation widget`__ : Learn how to display your devices with the latest telemetry data on the Trip Animation widget and modify the widget properties.

.. __: https://thingsboard.io/docs/iot-video-tutorials/#dashboard-development-guide-part-1-of-3-visualizing-assets-data-using-maps-and-tables
.. __: https://thingsboard.io/docs/iot-video-tutorials/#dashboard-development-guide-part-2-of-3-dashboard-states-aliases-and-widget-actions
.. __: https://thingsboard.io/docs/iot-video-tutorials/#dashboard-development-guide-part-3-of-3-remote-device-control-and-alarm-management
.. __: https://thingsboard.io/docs/iot-video-tutorials/#widget-configuration-guide-part-1-of-3-basic-settings
.. __: https://thingsboard.io/docs/iot-video-tutorials/#widget-configuration-guide-part-2-of-3-latest-values-map-widget
.. __: https://thingsboard.io/docs/iot-video-tutorials/#widget-configuration-guide-part-3-of-3-time-series-map-widget
.. __: https://thingsboard.io/docs/user-guide/ui/trip-animation-widget

* ThingsBoard Contribution and Development
    * `Widgets Development Guide`__ : Learn how to customize and create custom widgets.

.. __: https://thingsboard.io/docs/user-guide/contribution/widgets-development/
