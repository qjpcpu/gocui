GOCUI - Go Console User Interface
=================================

Minimalist Go library aimed at creating Console User Interfaces.

Installation
------------
	go get github.com/qjpcpu/gocui

Documentation
-------------
	godoc github.com/qjpcpu/gocui

Example
-------
	func layout(g *gocui.Gui) error {
		maxX, maxY := g.Size()
		if v, err := g.SetView("center", maxX/2-10, maxY/2, maxX/2+10, maxY/2+2); err != nil {
			if err != gocui.ErrorUnkView {
				return err
			}
			fmt.Fprintln(v, "This is an example")
		}
		return nil
	}
	func quit(g *gocui.Gui, v *gocui.View) error {
		return gocui.ErrorQuit
	}
	func main() {
		var err error
		g := gocui.NewGui()
		if err := g.Init(); err != nil {
			log.Panicln(err)
		}
		defer g.Close()
		g.SetLayout(layout)
		if err := g.SetKeybinding("", gocui.KeyCtrlC, 0, quit); err != nil {
			log.Panicln(err)
		}
		err = g.MainLoop()
		if err != nil && err != gocui.ErrorQuit {
			log.Panicln(err)
		}
	}
