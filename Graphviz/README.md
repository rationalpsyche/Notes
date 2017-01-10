# Graphviz

Compile:
`dot file.dot -T jpg -o name`

Example:

```
graph Films {
	{ node [shape=ellipse] "Eastern promises" "The Road" }
	{ node [shape=box] "Cronenberg"}
	{ node [shape=circle] "Viggo Mortensen"}

	{ edge [color="#2566ED",style="bold"] 
	"Cronenberg" -- "Eastern promises"
	}

	{ edge [color="#C7850B",style="solid"]
	"The Road" -- "Viggo Mortensen"
	"Eastern promises" -- "Viggo Mortensen"
	}
}
```

Shapes:
* ellipse
* box
* circle
* egg

Styles:
* bold
* solid
* dashed
* dotted