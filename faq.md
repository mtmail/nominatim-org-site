---
layout: page
permalink: /faq
---

## Frequently asked questions about Nominatim

### 1. The address of my search results contains far-away places that don't belong there. {#far-away-places}

Nominatim computes the address from two sources in the OpenStreetMap data:
from administrative boundaries and from place nodes. Boundaries are the more
useful source. They precisely describe an area. So it is very clear for
Nominatim if a point belongs to an area of not. Place nodes are more complicated.
These are only points without any precise extend. So Nominatim has to take a
guess and assume that an address belongs to the closest place nose it can find.
In an ideal world, Nominatim would not need the place nodes but there are
many places on earth where there are not precise boundaries available for
all parts that make up an address. This is in particular true for the more
local address parts, like villages and suburbs. Therefore it is not possible
to completely dismiss place nodes. And sometimes they sneak in where they
don't belong.

As a OpenStreetMap mapper, you can improve the situation in two ways: if you
see a place node for which already an administrative area exists, then you
should _link_ the two by adding the node with a 'label' role to the boundary
relation. If there is no administrative area, you can add the approximate
extend of the place and tag it place=<something> as well.

### 2. When doing reverse search, the address details have parts that don't contain the point I was looking up. {#point-outside-address}

There is a common misconception how the reverse API call works in Nominatim.
Reverse does not give you the address of the point you asked for. Reverse
returns the closest object to the point you asked for and then returns the
address of that object. Now, if you are close to a border, then the closest
object may be across that border. When Nominatim then returns the address,
contains the county/state/country across the border.

### 3. I get different counties/states/countries when I change the zoom parameter in the reverse query. How is that possible? {#address-and-zoom}

This is basically the same problem as in the previous answer.
The zoom level influences at which [search rank](https://wiki.openstreetmap.org/wiki/Nominatim/Development_overview#Country_to_street_level) Nominatim starts looking
for the closest object. So the closest house number maybe on one side of the
border while the closest street is on the other. As the address details contain
the address of the closest object found, you might sometimes get one result,
sometimes the other for the closest point.

