# teslajson
Simple Python class to access the Tesla JSON API.

Written by Greg Glockner

## Description
This is a simple Python interface to the [Tesla JSON
API](http://docs.timdorr.apiary.io/). With this, you can query your
vehicle, control charge settings, turn on the air conditioning, and
more.  You can also embed this into other programs to automate these
controls.

The class is designed to be simple.  You initialize a _Connection_
object, retrieve the list of _Vehicle_ objects, then perform get/set
methods on a _Vehicle_.  There is a single get method
[_Vehicle.get\_data()_] and a single set method [_Vehicle.command()_] so
that the class does not require changes when there are minor updates
to the underlying JSON API.

This has been tested with Python 2.7 and Python 3.2.  It has no dependencies
beyond the standard Python libraries.

## Installation
0. Download the repository zip file and uncompress it
0. Run the following command with your Python interpreter: `python setup.py install`

Alternately, add the teslajson.py code in your own program.

## Public API
`Connection(email, password, **kwargs)`:
Initialize the connection to the Tesla Motors website.

Required parameters:

- _email_: your login for teslamotors.com
- _password_: your password for teslamotors.com

Optional parameters:

- _url_: the base URL for the API
- _api_: API string
- _client\_id_: API identifier
- _client\_secret_: Secret API identifier

`Connection.vehicles`: A list of Vehicle objects, corresponding to the
vehicles associated with your account on teslamotors.com.

`Vehicle`: The vehicle class is a subclass of a Python dictionary
(_dict_).  A _Vehicle_ object contains fields that identify your
vehicle, such as the Vehicle Identification Number (_Vehicle['vin']_). 
All standard dictionary methods are supported.

`Vehicle.wake()`: Wake the vehicle.

`Vehicle.get_data(name)`: Retrieve data values specified by _name_, such
as _charge\_state_, _climate\_state_, _vehicle\_state_. Returns a
dictionary (_dict_).  For a full list of _name_ values, see the _GET_
commands in the [Tesla JSON API](http://docs.timdorr.apiary.io/).

`Vehicle.command(name)`: Execute the command specified by _name_, such
as _charge\_port\_door\_open_, _charge\_max\_range_. Returns a
dictionary (_dict_).  For a full list of  _name_ values, see the _POST_ commands
in the [Tesla JSON API](http://docs.timdorr.apiary.io/).

## Example
	import teslajson
	c = teslajson.Connection('youremail', 'yourpassword')
	v = c.vehicles[0]
	v.wake()
	v.get_data('charge_state')
	v.command('charge_start')

## Credits
Many thanks to [Tim Dorr](http://timdorr.com) for documenting the Tesla JSON API.
This would not be possible without his work.

## Disclaimer
This software is provided as-is.  This software is not supported by or
endorsed by Tesla Motors.  Tesla Motors does not publicly support the
underlying JSON API, so this software may stop working at any time.  The
author makes no guarantee to release an updated version to fix any
incompatibilities.