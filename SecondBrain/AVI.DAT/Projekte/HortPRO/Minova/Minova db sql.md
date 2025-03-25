## Overview devices and their locations

```sql
 select d.id, d.inventoryId, d.created as deviceCreated, l.created as linkCreated, o.url, o.created as locationCreated from devices as d left join device_to_location as l on d.id = l.deviceId left join locations as o on l.locationId = o.id;
```