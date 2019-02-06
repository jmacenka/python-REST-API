# Device Registry Service

## Usage

All responses will have the form

```json
{
  "data" : "mixed type holding the content of the response",
  "message" : "meta-data of what happened"
}
```

Subsequent response definitions will only detail the expected value of the `data field`

### List all devices

**Definition**

'GET /devices'

**Response**

- `200 OK` on success

```json
[
  {
    "identifier" : "bathroom-lamps-lamp1",
    "name" : "Bathroom main light",
    "device_type" : "switch",
    "controller_gateway" : "192.168.2.xxx"
  },
  {
    "identifier" : "kitchen-power-power1",
    "name" : "Kitchen - Oven power plug",
    "device_type" : "switch",
    "controller_gateway" : "192.168.2.xxx"
  }
]
```

### Registering a new device

**Definition**

`POST /devices`

**Arguments**

- `"identifier":string` a globally unique identifier for this device
- `"name":string` a friendly name for this device
- `"device_type":string` the type of device as understood by the client
- `"controller_gateway":string` the IP address of the device's controller

If a device with the given identifier already exists, the existing device will be overwritten.

**Response**

- `201 Created` on success

```json
{
  "identifier" : "kitchen-power-power1",
  "name" : "Kitchen - Oven power plug",
  "device_type" : "switch",
  "controller_gateway" : "192.168.2.xxx"
}
```

## Lookup device details

`GET /device/<identifier>`

**Response**

- `404 Not Found` if the device does not exist
- `200 OK` on success

```json
{
  "identifier" : "kitchen-power-power1",
  "name" : "Kitchen - Oven power plug",
  "device_type" : "switch",
  "controller_gateway" : "192.168.2.xxx"
}
```

## Delete a device

**Definition**

`DELETE /devices/<identifier>`

**Response**

- `404 Not Found` if the device does not exist
- `204 No Content` if the device has been deleted
