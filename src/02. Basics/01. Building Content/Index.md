# Building Content

Piranha CMS has three primary content types, **Pages**, **Posts** and **Sites**. You can read more about them and what's specific about them in their respective article. In this article we will cover the common components used to build these types and when you should use which type.

## Blocks

> Blocks should be used for pieces of content that can occur **any number of times**, at **any position** in the main content area. For fixed elements with a fixed number of occurrences Regions are a better match.

Blocks are the main building piece for **pages** and **posts**, it's the part of the content that the editor has total control over. Blocks are small chunks of content that can be added, deleted and reordered. As the content administrators choose for themselves which blocks they add you don't specify anywhere on the Content Type which blocks to use.

To read about the different block types that are available out-of-the box, please refer to [Standard Blocks](standard-blocks). For information on how to build your own blocks, please refer to [Custom Blocks](../extensions/custom-blocks).

## Regions

> Regions should be used for **fixed occurrences** of data on a Content Type, for example a Banner that always appear on the top. For content that can be placed anywhere in the content and occur any number of times Blocks are recommended.

Regions are the top-most level you can use to structure the different pieces of content. They are very flexible and can be configured in several ways, for example:

* A **single** field region - for main content regions
* A **composite** region made up of several fields
* A sortable **collection** of both of the above.

### Single Field Regions

When defining single field regions, the field type **must** be referenced directly from the Content Model. The deserializer **does not** support custom objects with a single field.

#### Correct Implementation

    using Piranha.AttributeBuilder;
    using Piranha.Models;

    [PageType]
    public class MyPage : Page<MyPage>
    {
        [Region]
        public HtmlField Body { get; set; }
    }

#### Incorrect Implementation

    using Piranha.AttributeBuilder;
    using Piranha.Models;

    public class MyBody
    {
        [Field]
        public HtmlField Body { get; set; }
    }

    public class MyPage : Page<MyPage>
    {
        [Region]
        public MyBody HtmlBody { get; set; }
    }

### Region Properties

When defining a region with the `RegionAttribute` you can set the following properties. Please note that all of these are totally optional.

#### Title

Optional title to be shown in the manager interface. If this property is left empty the **property name** is used. The example below shows a single field region in a Content Type.

    [Region(Title = "Main Content")]
    public MarkdownField MainContent { get; set; }

#### ListTitle

The optional **field name** of a composite region that should be used when rendering the collapsed list items in the manager interface. The example below shows a **composite region** that is made up of a `StringField` and a `TextField`.

    public class MyRegion
    {
        [Field]
        public StringField Title { get; set; }

        [Field]
        public TextField Body { get; set; }
    }

    ...

    [Region(ListTitle = "Title")]
    public IList<MyRegion> Teasers { get; set; }

#### ListExpand

If the list item should be expandable or if the fields should be shown directly in the list. The default behavior is `true` but it can be useful to set it to `false` if you have a single field region or a very simple list region. The example below will create a list of image fields and show them directly in the list.

    [Region(ListExpand = false)]
    public IList<ImageField> Images { get; set; }

#### SortOrder

Optional sort order. This can be useful if you want to inherit a base class containing regions and you want to force them into being displayed in a certain way in the manager interface. The default sort order is in the order they are declared in the class.

    [Region(SortOrder = 1)]
    public StringField Title { get; set; }

#### Icon

`[ This feature was added in version 7.0 ]`

The CssClass for the icon that should be used when rendering the region in the manager.

    [Region(Icon = "fas fas-fish")]
    public StringField Title { get; set; }

#### Display

`[ This feature was added in version 7.0 ]`

Defines how the region should be rendered in the manager. The following options are available to choose from:

* **Content** - Displays the region in the content region of the page with a selection button.
* **Setting** - Displays the region in the settings modal in its own tab
* **Hidden** - The region is not rendered. This should be used if it's part of a custom editor.

Remember that it has to make sense to define regions as `Settings`, otherwise the content editors will most likely not find it when editing the content.

    [Region(Display = RegionDisplayMode.Setting)]
    public MySeoInfo Seo { get; set; }

#### Region Description

Optional description that is shown above the region in the manager. This can be used to provide guidance and help to content editors when editing content.

    public class MyRegion
    {
        [Field]
        public StringField Title { get; set; }

        [Field]
        public TextField Body { get; set; }
    }

    [Region]
    [RegionDescription("Optional header shown at the top of the page.")]
    public MyRegion MyHeader { get; set; }

## Fields

> Fields are the lowest level of content in Piranha CMS and are used to build up `Regions` and `Blocks`. You can think of Fields as the different data types that you can use to build structures with. When defining a field in your `Region` or `Block` you can set the following properties with the `FieldAttribute`.

### Field Properties

#### Title

Optional title to be shown in the manager interface. If this property is left empty the **property name** is used.

    public class MyRegionarbitrary
    {
        [Field(Title = "The Title")]
        public StringField Title { get; set; }

        [Field]
        public TextField Body { get; set; }
    }

#### Options

A set of flags defining additional field behavior. At the moment the only flag available is `HalfWidth` which tells the manager interface that the field should only take up 50% of the available space so that another field can be display next to it.

    public class MyRegion
    {
        [Field(Options = FieldOption.HalfWidth)]
        public StringField Title { get; set; }

        [Field(Options = FieldOption.HalfWidth)]
        public StringField SubTitle { get; set; }

        [Field]
        public TextField Body { get; set; }
    }

#### Placeholder

Optional placeholder text. The placeholder text is shown for `CheckBoxField`, `DateField`, `NumberField` and `StringField`. For the CheckBox Field the placeholder text is shown as the checkbox **label**.

    [Field(Placeholder = "Please enter your full name")]
    public StringField Name { get; set; }

#### Field Description

`[ This feature was added in version 7.0 ]`

Optional description that is shown above the field in the manager. This can be used to provide guidance and help to content editors when editing content.

    [Field]
    [FieldDescription("Full street address including zip code")]
    public StringField Address { get; set; }

For a complete description of the available field types, please refer to [Standard Fields](standard-fields).