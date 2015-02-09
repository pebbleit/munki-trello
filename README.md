# Usage

# Troubleshooting

> I'm seeing items that won't move to the next stage no matter how often I move them.

Make sure the combination of ``name`` and ``version`` is unique. For speed, the initial ingest of Munki data is done via your ``all`` catalog rather than traversing your pkgsinfo files. Of you have two pkgsinfo files that have the same version / name combination as anther, this script won't touch anything after the first. Once the duplicate(s) have been removed, the item will be promoted to the next stage.