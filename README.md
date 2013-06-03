#### List Item Custom `ViewGroup` Example

This is the code example to go with a subtopic of the [Clean Code in Android
Apps][1] talk I gave at XebiCon 2013. It demonstrates why I recommend using a
custom `ViewGroup` for your `ListView`'s child views.

The app itself is a simple contacts list. It's implemented as a `ListView` with
a single kind of child view. There's a little bit of conditional logic in the
presentation of the list items:

* The email and street address fields are not shown if they have no data.
* If there's no name in the `Contact` record, the email address is shown in the
  name field and the email address field is not shown.
* If there's neither a name nor an email address in the `Contact` record, a
  default value is shown in the name field.

It turns out that even these three simple rules make for a sizeable blot of
code. This is not pretty code, but it's pretty unavoidable. Essential
complexity.

You should start by checking out the **1-_naieve_adapter** branch. This serves
as the "bad" example, where all the conditional logic is right inside the
`getView(..)` method. The `Adapter` class mixes the *View* and *Controller*
responsibilities indiscriminately.

The **2-_ViewHolder_pattern** branch demonstrates how using a `ViewHolder`
doesn't really change anything. It's a performance optimization to avoid
unnecessary calls of `findViewById(int)`, but the adapter class still mixes
responsibilities and `getView(..)` is still a mess.

Finally, the **3-_custom_ViewGroup** branch shows the approach I advocate. It
has a number of benefits:

* The `getView(..)` method is now very straight forward and the `Adapter` class
  is much cleaner. The clarity gains grow exponentially with the number of
  different view types the `Adapter` presents, in this case just one.
* The presentation rules for the list item are implemented within the new
  `ContactView` class.  It's no prettier, but it's isolated from all the other
  things and in the tightest scope it needs to be aware of.
* A `ViewHolder` is not needed, the `View` references are cached implicitly.

[1]: http://www.xebicon.nl/workshops/clean-code-in-android-apps

#### License

Copyright 2013 Xebia Nederland B.V.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

