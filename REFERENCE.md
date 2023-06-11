# Reference

<!-- DO NOT EDIT: This document was generated by Puppet Strings -->

## Table of Contents

### Classes

#### Public Classes

* [`freeradius`](#freeradius): Manage FreeRADIUS

#### Private Classes

* `freeradius::config`: Manage FreeRADIUS configuration.
* `freeradius::install`: Install the FreeRADIUS packages.
* `freeradius::service`: Manage the FreeRADIUS service

### Defined types

* [`freeradius::client`](#freeradiusclient): A short summary of the purpose of this defined type.
* [`freeradius::user`](#freeradiususer): Manage freeradius users

## Classes

### <a name="freeradius"></a>`freeradius`

This module manages the FreeRADIUS package, service, and a tiny bit
of configuration.

#### Examples

##### 

```puppet
include freeradius
```

#### Parameters

The following parameters are available in the `freeradius` class:

* [`users`](#users)
* [`packages`](#packages)
* [`service`](#service)
* [`config_owner`](#config_owner)
* [`config_group`](#config_group)
* [`config_mode`](#config_mode)
* [`config_dir`](#config_dir)
* [`clients`](#clients)

##### <a name="users"></a>`users`

Data type: `Hash`

A hash of concat::fragment resources used for building the
conf-module/files/authorize file containing users. The "target" is
set, you should provide "content" or "source", as well as "order".

Default value: `{}`

##### <a name="packages"></a>`packages`

Data type: `Array[String]`

The list of packages to install. Defaults from module data to
match OS family.

##### <a name="service"></a>`service`

Data type: `String`

The service to manage. Defaults from module data to match OS
family.

##### <a name="config_owner"></a>`config_owner`

Data type: `String`

The user owning the configuration file. Defaults from module data
to match OS family.

##### <a name="config_group"></a>`config_group`

Data type: `String`

The group owning the configuration file. Defaults from module data
to match OS family.

##### <a name="config_mode"></a>`config_mode`

Data type: `String`

The permissions on the configuration files. Defaults from module
data to match OS family.

##### <a name="config_dir"></a>`config_dir`

Data type: `Stdlib::Absolutepath`

The root of the configuration directory. Defaults from module
data to match OS family.

##### <a name="clients"></a>`clients`

Data type: `Hash`



Default value: `{}`

## Defined types

### <a name="freeradiusclient"></a>`freeradius::client`

A description of what this defined type does

#### Examples

##### 

```puppet
freeradius::client { 'box':
  attributes => {
    ipaddr => '2001:db8::/64',
    secret => 'changeme',
  }
}
```

#### Parameters

The following parameters are available in the `freeradius::client` defined type:

* [`attributes`](#attributes)
* [`client`](#client)

##### <a name="attributes"></a>`attributes`

Data type: `Hash[String, String]`

Client attributes. See
https://freeradius.org/radiusd/man/clients.conf.html for
documentation.

Default value: `{}`

##### <a name="client"></a>`client`

Data type: `String`



Default value: `$title`

### <a name="freeradiususer"></a>`freeradius::user`

Manage freeradius users. This creates a fragment added to the
authorize file.

#### Examples

##### 

```puppet
freeradius::user { 'bob':
  content => "\"bob\" Cleartext-Password == \"changeme\"\n"
}
freeradius::user { 'DEFAULT':
  order   => 01,
  content => "\"bob\" Cleartext-Password == \"changeme\"\n",
}
```

#### Parameters

The following parameters are available in the `freeradius::user` defined type:

* [`order`](#order)
* [`content`](#content)
* [`user`](#user)

##### <a name="order"></a>`order`

Data type: `Optional[Variant[String,Integer]]`

Optional parameter for concat::fragment.

Default value: ``undef``

##### <a name="content"></a>`content`

Data type: `String`

Text content for the user definition. See
https://freeradius.org/radiusd/man/users.txt for format
documentation.

##### <a name="user"></a>`user`

Data type: `String`



Default value: `$title`
