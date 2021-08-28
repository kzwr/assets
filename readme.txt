API
constructor([el][, options])

    Arguments:

      el {String | HTMLElement}['']       selector or html element
      options {Object} [{...}]             options for watermark
        textArray {Array} [['example']]   text list to display`
        fontSize {Number} [26]            font size`
        fontFamily {String} ['serif']     font family`
        padding {Number} [25]             watermark wrapper padding with text`
        lineHeight {Number} [-1]          text line height`
        rotate {Number} [0]               the angle of rotate, must in range of (-PI/2, PI/2)
        fontScale {Number} [0.5]          Half-width and full-width fonts width ratio
        color {String} ['#eeeeee']        text color
        auto {Boolean} [true]             whether add background to mounted element automatically
        observe {Boolean} [true]          whether observe background of mounted element

    Example:

        new Watermark();

        new Watermark('body', {
          textArray: [
            'example',
            '你好，欢迎使用',
            'Hello, 世界'
          ],
          fontSize: 16,
        });

    Note: If you set options.auto = false, Watermark will never add background to the mounted element, you must do it manually. for example:

      /*
       * use api
       */
      const watermark = new Watermark('body', { auto: false });
      // ... do some action
      watermark.draw();
      // you can access canvas by watermark.canvas properity
      watermark.render();   // must after draw call

      /*
       * use pure js
       */
      const watermark = new Watermark('body', {
        auto: false,
      });
      watermark.draw();
      const canvas = watermark.draw().canvas;
      const dataUrl = canvas.toDataURL();
      const body = document.body;
      body.style.background = `url(${dataUrl})`;

mount(el)

    Arguments:
        el {String | HTMLElement} selector or html element

    Usage:

    If a watermark instance not mount any element when is was created, you can use mount function to mount a element for it.

    Example:

        const watermark = new Watermark({
          color: '#cccccc'
        }); // create a instance of Watermark
        watermark.mount('body');  // mount to document.body
        // watermark.draw();  // dont fotget to use draw() to display watermark on mounted element

set(options)

    Arguments:
        options {Object}[{...}] options for watermark

    Usage:

    It's default value is same as constructor You can use set function to re-configurate watermark style

    Example:

          const watermark = new Watermark('body', {
            // your options
          });
          // if you want to re-configurate
          watermark.set({
            // your new options
          });
          // watermark.draw();  must use draw() to display

draw()

    Usage:

    use this function to render watermark on the mounted element.

    Example:

        new Watermark('body').draw();

        new Watermark().set().mount().draw();

        new Watermark('body').set().draw();

destroy()

    Usage:
        unmount element
        disconnect mutation observer
        change options to default value

    Example:

        new Watermark().set().mount().destroy();

render()

    Usage:
        add background to mounted element

    Note:
        only used in situation that options.auto is setted to false

observer()

    Usage:
        add observer that can observe background of mounted element

    Note:
        only used in situation that options.observe is setted to false
