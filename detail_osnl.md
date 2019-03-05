---
layout: contents
language: en-us
title: K2HR3 OSNL
short_desc: overview and details on k2hr3_osnl 
lang_opp_file: detail_osnlja.html
lang_opp_word: To Japanese
prev_url: 
prev_string: 
top_url: detail.html
top_string: Detail
next_url: detail_various.html
next_string: Various
---

# Details of K2HR3 OpenStack Notification Listener

This page describes how K2HR3 OpenStack Notification Listener works in detail.

K2HR3 OpenStack Notification Listener is a daemon process to synchronize the OpenStack 'instance' metadata between OpenStack and K2HR3. To catch a new notification, it listens to a queue in a messaging backend where messages sent by OpenStack services are delivered.

![K2HR3 OSNL overview](images/detail_osnl.png)

## OpenStack Notification Listener

This chapter describes the [OpenStack Notification Listener](https://docs.openstack.org/oslo.messaging/latest/reference/notification_listener.html) behavior.

[OpenStack Notification Listener](https://docs.openstack.org/oslo.messaging/latest/reference/notification_listener.html) listens to notification messages from OpenStack services. However, OpenStack services, notifiers, don't directly send notification messages to [OpenStack Notification Listener](https://docs.openstack.org/oslo.messaging/latest/reference/notification_listener.html). Here is the general delivery flow of notification messages from notifiers to listeners.

* Notifiers emit notification messages to a messaging backend when events to be notified for the others happen.
  * They use messaging drivers, which are defined by [oslo.messaging](https://docs.openstack.org/oslo.messaging/latest/), to publish notification messages.
	* Notification messages are guaranteed not to be duplicated because they are sent ‘at-most-once’.
  * The messaging drivers determine the each notification message format.
	* The messages driver must be either the *messaging* or the *messagingv2*.
	* The notifier's configuration determines the message driver.
* Notifiers publish each message with a *topic* and an *exchange*.
  * The *topic* is used as a routing key in a messaging backend.
	* The message backend determines a queue where the message is delivered by using the *topic*.
  * The *exchange* is a valid scope of the message, which can be used to restriction access to the message.
  * See [Environments and Settings](environments.html) for the listener settings of the *topic* and the *exchange*.
* A messaging backend will receive notification messages and then distribute the copies to destination queues using rules called 'bindings'.
  * Message queues are where notification messages are delivered by a messaging backend.
  * The messaging backend then deliver a message to one randomly selected [OpenStack Notification Listener](https://docs.openstack.org/oslo.messaging/latest/reference/notification_listener.html). 
* The selected [OpenStack Notification Listener](https://docs.openstack.org/oslo.messaging/latest/reference/notification_listener.html) will parse the message by using a exposed function which corresponds to the message's priority. 
  * For example, a message priority is 'info', the listener invoke the 'info' function of its own.

## K2HR3 OpenStack Notification Listener

This chapter describes the 'K2HR3 OpenStack Notification Listener' behavior.

K2HR3 OpenStack Notification Listener is a plugin of [OpenStack Notification Listener](https://docs.openstack.org/oslo.messaging/latest/reference/notification_listener.html). The following figure shows the overview of the plugin, which describes that:

* It consumes messages in the message backend.
  * The message contains the metadata of the deleted instance.
* It parses the message.
  * The plugin finds the unique id and the IP address of the deleted instance.
* It calls the delete method of the K2HR3's [Role API](api_role.html) with them.


![K2HR3 OSNL details](images/detail_osnl_details.png)

Here are the primary settings parameters to control the plugin's behavior. 

* transport_url
  * This parameter value represents the transport configuration parameters in the form of a URL.
  * Transport URLs take the form:
	* **transport://user:pass@host1:port[,hostN:portN]/virtual_host** 
    * See the [oslo.messaging's Transport](https://docs.openstack.org/oslo.messaging/latest/reference/transport.html#oslo_messaging.TransportURL) for details.
	  * ex) rabbit://guest:guestpass@127.0.0.1:5672/
		  * [RabbitMQ](http://www.rabbitmq.com/) is a messaging backend.
		  * `guest` is the username to login the messaging backend.
		  * `guestpass` is the password to login the messaging backend.
		  * `localhost` is the host name to login.
		  * `5672` is the port number of the host.
* topic
  * The parameter determines the queue name to be delivered the notification messages to.
	* It is used as a routing key in a messaging backend.
  * This parameter is required when each OpenStack service publishes notification messages.
  * *notifications* is the default value in K2HR3.
	* The messaging priority will be added at the end of the topic name to the actual queue name.
* exchange
  * This parameter determines a valid scope of a notification message.
  * *neutron* is the default value in K2HR3.

To know how to configure the plugin, see the [Environments and Settings](environments.html) page.

To parse messages and find enough information to call the K2HR3's [Role API](api_role.html], the values of the 'topic' and the 'exchange' must be configured with the same with notifiers target destination settings. See the [Environments and Settings](environments.html) page for the plugin settings.

