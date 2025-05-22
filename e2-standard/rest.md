POST https://compute.googleapis.com/compute/v1/projects/gen-lang-client-0537114074/zones/europe-north2-b/instances
{
  "canIpForward": false,
  "confidentialInstanceConfig": {
    "enableConfidentialCompute": false
  },
  "deletionProtection": false,
  "description": "",
  "disks": [
    {
      "autoDelete": true,
      "boot": true,
      "deviceName": "auth-server",
      "initializeParams": {
        "diskSizeGb": "10",
        "diskType": "projects/gen-lang-client-0537114074/zones/europe-north2-c/diskTypes/pd-balanced",
        "labels": {},
        "sourceImage": "projects/debian-cloud/global/images/debian-12-bookworm-v20250513"
      },
      "mode": "READ_WRITE",
      "type": "PERSISTENT"
    }
  ],
  "displayDevice": {
    "enableDisplay": false
  },
  "guestAccelerators": [],
  "instanceEncryptionKey": {},
  "keyRevocationActionType": "NONE",
  "labels": {
    "goog-ec-src": "vm_add-rest"
  },
  "machineType": "projects/gen-lang-client-0537114074/zones/europe-north2-b/machineTypes/e2-medium",
  "metadata": {
    "items": []
  },
  "name": "auth-server",
  "networkInterfaces": [
    {
      "accessConfigs": [
        {
          "name": "External NAT",
          "networkTier": "PREMIUM"
        }
      ],
      "stackType": "IPV4_ONLY",
      "subnetwork": "projects/gen-lang-client-0537114074/regions/europe-north2/subnetworks/default"
    }
  ],
  "params": {
    "resourceManagerTags": {}
  },
  "reservationAffinity": {
    "consumeReservationType": "ANY_RESERVATION"
  },
  "scheduling": {
    "automaticRestart": true,
    "onHostMaintenance": "MIGRATE",
    "provisioningModel": "STANDARD"
  },
  "serviceAccounts": [
    {
      "email": "157389917745-compute@developer.gserviceaccount.com",
      "scopes": [
        "https://www.googleapis.com/auth/devstorage.read_only",
        "https://www.googleapis.com/auth/logging.write",
        "https://www.googleapis.com/auth/monitoring.write",
        "https://www.googleapis.com/auth/service.management.readonly",
        "https://www.googleapis.com/auth/servicecontrol",
        "https://www.googleapis.com/auth/trace.append"
      ]
    }
  ],
  "shieldedInstanceConfig": {
    "enableIntegrityMonitoring": true,
    "enableSecureBoot": false,
    "enableVtpm": true
  },
  "tags": {
    "items": []
  },
  "zone": "projects/gen-lang-client-0537114074/zones/europe-north2-b"
}

POST https://compute.googleapis.com/compute/v1/projects/gen-lang-client-0537114074/regions/europe-north2/resourcePolicies
{
  "name": "default-schedule-1",
  "region": "europe-north2",
  "snapshotSchedulePolicy": {
    "retentionPolicy": {
      "maxRetentionDays": 14,
      "onSourceDiskDelete": "KEEP_AUTO_SNAPSHOTS"
    },
    "schedule": {
      "dailySchedule": {
        "daysInCycle": 1,
        "startTime": "14:00"
      }
    },
    "snapshotProperties": {
      "guestFlush": false,
      "labels": {}
    }
  }
}

POST https://compute.googleapis.com/compute/v1/projects/gen-lang-client-0537114074/zones/europe-north2-b/disks/auth-server/addResourcePolicies
{
  "resourcePolicies": [
    "projects/gen-lang-client-0537114074/regions/europe-north2/resourcePolicies/default-schedule-1"
  ]
}
