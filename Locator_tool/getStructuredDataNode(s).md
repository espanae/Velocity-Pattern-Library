# Data Definition Fields

- [Checkboxes](#checkboxes)
- [Images](#images)
- [Groups](#groups)

## Checkboxes
data definition
```xml
<system-data-structure>
	<contentTypes>
		<value>Ordered List</value>
	</contentTypes>
```
Velocity
```
None of this works:

$p.getStructuredDataNode("contentTypes").textValue[0] [1]
Null

$p.getStructuredDataNode("contentTypes").textValues.get(1) .get(0)
An error occurred while rendering asset preview: org.apache.velocity.exception.MethodInvocationException: Invocation of method 'get' in  class [Ljava.lang.String; threw exception java.lang.ArrayIndexOutOfBoundsException at velocityTransform-1516635641980[line 43, column 57]

$p.getStructuredDataNode("contentTypes").textValues[1]
An error occurred while rendering asset preview: org.apache.velocity.exception.VelocityException: Error invoking method 'get(java.lang.Integer)' in [Ljava.lang.String; at velocityTransform-1516635499601[line 42, column 56]

$p.getStructuredDataNode("contentTypes").textValues[0]
## Output: An error occurred while rendering asset preview: org.apache.velocity.exception.VelocityException: Error invoking method 'get(java.lang.Integer)' in [Ljava.lang.String; at velocityTransform-1516634650518[line 42, column 56]

$p.getStructuredDataNode("contentTypes").textValues
## Output: [Ljava.lang.String;@463513e6

$p.getStructuredDataNode("contentTypes").textValues.size()
1

$_PropertyTool.outputProperties($p.getStructuredDataNode("contentTypes").TextNodeOptions )
Properties:
 - dropdown: boolean
 - radio: boolean
 - calendar: boolean
 - checkbox: boolean
 - wysiwyg: boolean
 - datetime: boolean
 - plainText: boolean
 - multiselect: boolean


$p.getStructuredDataNode("contentTypes").TextNodeOptions.Checkbox
## true
-----------------------------
velocity
## $currentPage.getStructuredDataNodes("contentTypes").get(0).Class.Name
## com.hannonhill.cascade.api.adapters.StructuredDataNodeAPIAdapter

## $currentPage.getStructuredDataNodes("contentTypes").get(0).getIdentifier()
## contentTypes

$currentPage.getStructuredDataNodes("contentTypes").get(0).textValues.size()
## 2

$currentPage.getStructuredDataNodes("contentTypes").get(0).textValues[1]
## Ordered List

## $_PropertyTool.outputProperties( $currentPage.getStructuredDataNodes("contentTypes").get(0) )
 Object type: com.hannonhill.cascade.api.adapters.StructuredDataNodeAPIAdapter
Properties:
 - group: boolean
 - asset: FolderContainedAsset
 - asset: boolean
 - assetType: String
 - assetIdentifier: PathIdentifier
 - textValues: String[]
 - identifier: String
 - group: StructuredDataNode[]
 - getChildren(String): StructuredDataNode[]
 - children: StructuredDataNode[]
 - text: boolean
 - textValue: String
 - identifer: Identifier
 - textValueAsXMLElement: Element
 - textNodeOptions: TextNodeOptions
 - getChild(String): StructuredDataNode
 - allowCustomValues: boolean
 - children: StructuredDataNode[]
 - getChildren(String): StructuredDataNode[]
 - text: boolean
 - group: StructuredDataNode[]
 - identifier: String
 - assetIdentifier: PathIdentifier
 - textValues: String[]
 - asset: FolderContainedAsset
 - group: boolean
 - persisted: boolean
 - asset: boolean
 - allowCustomValues: boolean
 - textNodeOptions: TextNodeOptions
 - getChild(String): StructuredDataNode
 - textValueAsXMLElement: Element
 - class: Class
 - textValue: String
```
## Images
Data Definition
```
<system-data-structure>
	<group identifier="iconpic" label="Main Page Image" collapsed="true">
		<asset type="file" identifier="image" label="Image"/>
  </group>
</system-data-structure>
```
Velocity
```
$currentPage.getStructuredDataNode("iconpic/image").Asset.Link
## Output: site://TDI/takefive/artwork/newyearstips-index.jpg
```
## Groups
Data Definition
```
<system-data-structure>
  <group identifier="newsandevents" label="News and Events" restrict-to-groups="news">
      <group identifier="item" label="Headline" restrict-to-groups="news">
          <text identifier="headline" label="Headline" restrict-to-groups="news" required="true"/>
          <text identifier="link" label="Link" restrict-to-groups="news" required="true"/>
          <asset type="file" identifier="image" label="Thumbnail (247 x 98)" required="true" help-text="Photo must be resized to the correct dimensions in Photoshop"/>
      </group>
  </group>
</system-data-structure>
```

Multiple groups
```
#set ( $item = $currentPage.getStructuredDataNodes("newsandevents/item").get(0) )
<img src="${item.getChild("image").getAsset().link}" />
<a href="${item.getChild("link").textValue}">
    ${_EscapeTool.xml( $item.getChild("headline").textValue )}
</a>
```
