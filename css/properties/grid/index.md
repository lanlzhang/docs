{{Page_Title}}
{{Flags
|State=In Progress
|Editorial notes=Add description, specifications, compatibility.
|Checked_Out=No
}}
{{Standardization_Status|W3C Working Draft}}
{{API_Name}}
{{Summary_Section|Foundation of a two-dimensional grid-based layout system.  Defines an element as part of a grid and permits those elements to be displayed differently than the flow order.  Also used as a shorthand for setting all the explicit grid properties ([[css/properties/grid-template-rows|grid-template-rows]], [[css/properties/grid-template-columns|grid-template-columns]], and [[css/properties/grid-template-areas|grid-template-areas]]), as well as all the implicit grid properties ([[css/properties/grid-auto-rows|grid-auto-rows]], [[css/properties/grid-auto-columns|grid-auto-columns]], and [[css/properties/grid-auto-flow|grid-auto-flow]]), in a single declaration. If the <grid-auto-rows> value is omitted, it is set to the value specified for grid-auto-columns. Other omitted values are set to their initial values.}}
{{CSS Property
|Initial value=See individual properties
|Applies to=Grid containers, Grid layout
|Inherited=No
|Media=visual
|Computed value=See individual properties
|Animatable=No
|CSS percentages=See individual properties
|Values={{CSS Property Value
|Data Type=<grid-template>
|Description=Itself a shorthand property, see [[css/properties/grid-template|grid-template]] for details.
}}{{CSS Property Value
|Data Type=<grid-auto-flow>
|Description=See [[css/properties/grid-auto-flow|grid-auto-flow]] for details.
}}{{CSS Property Value
|Data Type=<grid-auto-columns> / <grid-auto-rows>
|Description=See [[css/properties/grid-auto-columns|grid-auto-columns]] and [[css/properties/grid-auto-rows|grid-auto-rows]] for details.
}}
}}
{{Examples_Section
|Not_required=No
|Examples={{Single Example
|Language=CSS
|Code=#grid {
      display: grid;
      grid-template-columns: auto minmax(min-content, 1fr);
          grid-template-rows: auto minmax(min-content, 1fr) auto
  }
  #prdName    { grid-column: 1; grid-row: 1 }
  #grossPrice    { grid-column: 1; grid-row: 3 }
  #retailPrice   { grid-column: 1; grid-row: 2; justify-self: start }
  #discount    { grid-column: 2; grid-row: 1 / span 2; }
  #finalPrice { grid-column: 2; grid-row: 3; align-self: center}
}}
}}
{{Notes_Section}}
{{Related_Specifications_Section
|Specifications=
}}
{{Compatibility_Section
|Not_required=No
|Imported_tables=
|Desktop_rows=
|Mobile_rows=
|Notes_rows=
}}
{{See_Also_Section}}
{{Topics|CSS}}
{{External_Attribution
|Is_CC-BY-SA=No
|MDN_link=
|MSDN_link=
|HTML5Rocks_link=
}}