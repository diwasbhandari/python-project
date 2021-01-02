# Device Registry Service

## Usage

All responses will have the form
```json
{
  "data": "Mixed type holding the content of the response",
  "message": "Description of what happened"
}
```
Subsequent response definitions will only detail the expected value of the `data field`

### List all devices
**Definition**
`GET /devices`
**Response**
- `200 OK` on success
```json
[
  {
    "identifier": "floor-lamp",
    "name": "Floor Lamp",
    "device_type": "switch",
    "controller_gateway": "192.2.50.2"
  },
  {
    "identifier": "Sony-tv",
    "name": "Living Room TV",
    "device_type": "tv",
    "controller_gateway": "192.2.50.3"
  }
]
```
### Registering a new device
**Definition**
`POST /devices`
**Argument**
- `"identifier":string` a globally unique identifier for this device
- `"name":string` a friendly name for this device
- `"device_type":string` the type of the device as understood by the client
- `"controller_gateway":string` the IP address of the device's controller

If a device with the given identifier alreay exists, the existing device will be overwritten.
**Response**
-`201 Created` on success
```json
{
    "identifier": "floor-lamp",
    "name": "Floor Lamp",
    "device_type": "switch",
    "controller_gateway": "192.2.50.2"
  }
```
### Lookup device details
`GET /devices/<identifier>`
**Response**
- `404 Not Found` if the device does not exist
- `200 OK` on success
```json
{
    "identifier": "floor-lamp",
    "name": "Floor Lamp",
    "device_type": "switch",
    "controller_gateway": "192.2.50.2"
  }
```
### Delete a device
**Definition**
`DELETE /devices/<identifier>`
**Response**
- `404 Not Found` if the device does not exist
- `204 No Content`