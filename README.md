# IoT Perishable Goods Network



**Participants**
`Grower` `Importer` `Shipper`

**Assets**
`Contract` `Shipment`

**Transactions**
`TemperatureReading` `GpsReading` `ShipmentReceived` `SetupDemo`

**Events**
`TemperatureThresholdEvent` `ShipmentInPortEvent`

To test this Business Network Definition in the **Test** tab:

Submit a `SetupDemo` transaction:

```
{
  "$class": "org.oxxo.shipping.iot.SetupDemo"
}
```

This transaction populates the Participant Registries with a `Grower`, an `Importer` and a `Shipper`. The Asset Registries will have a `Contract` asset and a `Shipment` asset.

Submit a `TemperatureReading` transaction:

```
{
  "$class": "org.oxxo.shipping.iot.TemperatureReading",
  "centigrade": 8,
  "shipment": "resource:org.oxxo.shipping.iot.Shipment#SHIP_001"
}
```

If the temperature reading falls outside the min/max range of the contract, the price received by the grower will be reduced, and a `TemperatureThresholdEvent` is emitted. You may submit several readings if you wish. Each reading will be aggregated within `SHIP_001` Shipment Asset Registry.

Submit a `ShipmentReceived` transaction for `SHIP_001` to trigger the payout to the grower, based on the parameters of the `CON_001` contract:

```
{
  "$class": "org.oxxo.shipping.iot.ShipmentReceived",
  "shipment": "resource:org.oxxo.shipping.iot.Shipment#SHIP_001"
}
```

If the date-time of the `ShipmentReceived` transaction is after the `arrivalDateTime` on `CON_001` then the grower will no receive any payment for the shipment.

Submit a `GpsReading` transaction:

```
{
  "$class": "org.oxxo.shipping.iot.GpsReading",
  "readingTime": "120000",
  "readingDate": "20171024",
  "latitude":"40.6840",
  "latitudeDir":"N",
  "longitude":"-74.0062",
  "laongitudeDir":"W",
}
```

If the GPS reading indicates the ship's location is the Port of New Jersey/New York (40.6840,-74.0062) then a `ShipmentInPortEvent` is emitted.

Enjoy!
# logichain
