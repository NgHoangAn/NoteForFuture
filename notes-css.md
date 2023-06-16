# Selector
  + tìm kiếm html element
	+ type:
		name, id, class
		combinator
		pseudo-class
		pseudo-element
		attribute
	+ #id / .class / element.class / * / element / element, element...

# bg
  + -color

  + -image: url("")

  + -repeat
	+ no-reapeat
	+ repeat
	+ repeat-x
	+ repate-y

  + -position: position1 position2
	+ ko lặp và hiển thị ở vị trí nào đó
	+ pos1,pos2: top bot left center right

  + -attachment: value
	+ đứng im khi scroll
	+ value:
			  fixed       // đứng im
			  scroll    // di chuyển theo khi kéo

	+ -position

	+ -clip / origin / size

# color
	+ RGB / Hex / HSL / RGBA / HSLA

	+ RGB(red, green, blue) // [0-255]

	+ RGBA(red, green, blue, alpha) // anpha [0.0 - 1]

	+ HEX(#rrggbb) or (#rgb)  // [0-255]

	+ HLS(hue, saturation, lightness)
		+ hue [0-260] rgb/3
		+ saturation 0-100%
		+ lightness 0-100%

	+ HLSA
		+ anpha [0.0 - 1]

# border
  + style

  + width

  + color

  + border: width style color

  + radius

# margin
  + tạo k/trắng xung quanh element

  + value:
	+ auto:
	+ length
	+ %: dựa vào % chiều dài của p/tử chứa
	+ inherit: kế thừa margin của cha

# padding
  + tạo k/trắng bện trong element

  + dùng box-sizing: border-box để giữ nguyên width element (ko phụ thuộc vào pading, border, margin)

# height/width
	+ max-width: chiều aco tối đa của element

# box model
	+ bao gồm margin / padding / border / content

# outline
  + line drawn bên ngoài border

  + width

  + color

  + offset

# text
  + text color

  + text-align: 
	+căn chỉnh theo chiều ngang
	+ left / right / center / justify[các hàng có độ rộng = nhau, margin trái-phải thẳng]
	+ text-align-last: căn chỉnh dòng cuối

  + direction: thay đổi hướng text
	+ rtl: right -> left

  + vertical-align: căn chỉnh theo chiều dọc
	+ baseline
	+ text-top / text-bottom
	+ sub / super

  + text-decoration-
	+ line: overline / line-through / underline
	+ color:
	+ style: solid / dotted ....
	+ thickness: độ dày của line
		+ px, %

  + text-transform
	+ uppercase
	+ lowercase
	+ capitalize
  
  + text spacing
	+ text-indent: ...px  -> thụt lề dòng đầu
	+ letter-spacing: ...px -> k/cách giữa các kí tự
	+ line-height: ... -> space giữa lines
	+ word-spacing: ...px -> space word
	+ white-space: nowrap -> ko ngắt dòng
  
  + text-shadow: ...


# font
  + types:
	+ serif : có nét nhỏ ở các cạnh mỗi chữ
	+ sans-serif: clear các nét nhỏ -> tối giản (recomment)
	+ monospace: robot chữ
	+ cursive: same viết tay
	+ fantasy: decor-fun

  + font-family:              REQUIRE

  + font-style:
	+ normal / italic

  + font-weight:
	+ normal / bold

  + font-variant: chữ hoa
	+ normal / small-caps [chự in hoa hết, chữ hoa sẵn sẽ to hơn]

  + font-size                 REQUIRE
	+ default 16px = 1em
	+ 1vw = 1% viewport width

# icons
	+ <i> / <span>


# float
	left
	right
	none
	khi dùng float thì phần nối tiếp với thẻ chứa thẻ float sẻ bị thẻ float đè lên()-> dùng overflow:hidden trong thẻ cha chừa float

# link
  + color

  + :visited -> đã ghé qua

  + :hover   -> hover vào

  + :active  -> hine65 tại đang click

  + RULE
	  + :link -> :visited -> :hover -> :active

# list
  + list-style-type: circle / square / upper-roman / lower-alpha

  + list-style-image: url('')

  + list-style-position: outside / inside

# table
  + border-collapse: 2 viền thành 1

# Layout 

## display
  + block element
	+ <div>
	+ <h1> - <h6>
	+ <p>
	+ <form>
	+ <header> / <footer> / <section>

	+ luôn lấy full width avaliable

  + inline element
	  + <span> / <a> / <img>
	  + ko dung được margin:top/bottom 

  + display: none -> default

  + visibility: hidden;

  + hidden vs none
	+ hidden thì chỉ ẩn thôi, vẫn chiếm space

## width: 
  + ở block ngăn p/tử kéo dài ra các cạnh của container

  + sau đó dùng margin:auto để can9 giữa element theo chiều ngang trong container
	+ element chiếm width đã cho , spae còn lại chia đều cho 2 margin
	+ vấn đề : khi window nhỏ hơn width element -> xuất hiện thanh cuộn
				-> dung max-width để giải quyết
## position
  + static: default

  + relative: định vị với vị trí bình thường của nó
	+ left / right / top / bottom

  + fixed: định vị với viewport
	+ left / right / top / bottom
	+ mốc neo ko đổi

  + absolute: định vị so với element cha được định vị gần nhất
	+ nếu ko có cha được định vị thì sẽ dựa theo document body và di chuyển theo nếu như scroll
	+ position của element sẽ bị xóa và c1 thể overlap

  + sticky: định vị dựa trên scroll
	+ là sự chuyển đổi relative <=> fixed.
	+ phụ thuộc vào scroll position

  + clip
	+ tạo ra rect() được định vị absolute
	+ có 4 value từ góc top-left để tạo ra rect
	+ ko khả dụng với overflow:visible
  ========
  + static: mặc định
	relative: định vị tuyệt đối, các thẻ html bên ngoài coi nó là cha
	absolute: định vị tương đối theo thẻ cha or thẻ body nếu ko có khai báo
	fixed: định vị tương đối cho cửa sổ Bowser của trình duyệt
	inherit: thừa hưởng các thuộc tính từ t/phần cha
	- relativev là khung - absolute là con có thể di chuyển bên trong khung đến bất kỳ vị trí nào kể cả ngoài khung.

## z-index
  + chỉ định thứ tự sắp xếp của element

  + chỉ active trên các
	+ position(relative,absolute,fixed,sticky)
	+ flex item( element con của element display:flex)

  + nếu 2 position element bị chồng lên nhau mà ko có z-index thì cái nào sau sẽ được hiển thị đè lên cái trước

## overflow
  + control content khi quá lớn để vừa area

  + prop:
	  + visible DEFAULT
	  + hidden    -> phần tràn bị cắt và ẩn đi
	  + scroll    -> phần tràn bị cắt và khi scroll sẽ thấy được
	  + auto      -> giống scroll, sẽ thêm scrollbar khi cần thiết

  + chỉ active với block element có height

  + overflow-x
	  + thay đổi theo left/right

  + overflow-y
	  + thay đổi theo top/bottom

## float - clear
  + float: positioning và format content
	+ left / right / none / inherit[kế thừa float cha]

  + clear:
	+ khi dùng float cho 1 element và muốn element tiếp theo phải ở dưới element đó(ko phải left/right) -> dùng clear vào element next
	+ do something với next element
	+ prop
	  + left / right / both / none / inherit
	+ clearfix:
	  + khi float element cao hơn container chứa element
		+ element float sẽ bị overflow ra ngoài
		  -> dùng clearfix
			.clearfix::after{
				content:"";
				clear:both;
				display:table
			}
  + box-sizing:
	+ nếu tạo 3 box với width:33.33%, sau đó add padding và border --> bị vỡ
	+ bao gồm padding, border trong total width(height), miễn sao cho các prop luôn tồn tại trong box thì sẽ ko bị vỡ

## inline-block
    + cho phép set width/height so với inline ko được
  
    + có margin/padding top/bottom <=> inline ko có

    + có thể nằm trên 1 hàng <=> block phải khác hàng

## align
    + block element center theo chiều ngang -> margin:auto

    + center text inside element -> text-align: center

    + center image -> margin-left/right: auto (block element)

    + dùng absolute -> 

    + dùng float

    + căn theo chiều dọc -> padding cho top/bottom
                            -> line-height có value = height

    + căn theo cả 2:
        + padding + text-align: center; 



# combinators
  + (space)   -> chọn hậu duệ
	+ div p
	+ chọn all p là con/cháu/chắt của div

  + (>)       -> con trực thuộc
	+ div > p
	+ chọn all p là con TRỰC TIẾP từ div

  + (+)       -> chọn 1 anh/em ngay sau "KẾ BÊN NHÀ- SÁT NHÀ"
	+ div + p

  + (~)       -> chọn all anh/em ngay sau element

# pseudo-class
  + define trạng thái đặc biệt của element

  + selector:pseudo-class{
	  prop: value
  }

  + a pseudo-class
	+ link,visited > hover > active

  + :first-child pseudo-class / :last-child / :nth-child(n)
	+ p:first-child {...}
	+ p:first-child i {...} -> all i trong first p

  + :lang
	+ define rule of languages

  + :checked

  + :disabled / :enable

  + :empty

  + :first-of-type / :last-of-type / :nth-of-type(n) / :nth-lat-of-type(n)
	  -> chọn all element là first của cha

  + :focus / :target

  + :in-range     -> chọn all element trong range

  + :invalid / :valid

  + :read-only / :read-write

# pseudo-element
  + tạo kiểu cho các phần được chỉ định của element

  + selector::pseudo-element{...}

  + ::first-line
	+ làm gì đó với line đầu tiên của text
	+ active trên block
	+ prop apply
	  + font / color / bg / word-letter-spacing / text-decor / vertical-align / text-transform / line-height / clear

  + ::first-letter
	  + do something với chữ đầu của text
	  + active trên block
	  + prop apply
		  + font / color / bg / margin / padding / border / text-decor / text-transform / line-height / float /
		  clear / vertical-align(only if float is none)

  + ::before
	+ add some content trước element

  + ::after
	+ ad some content sau element

  + ::marker
	+ đánh dấu list items

  + ::selection
	+ tạo ra cái highlight O_*
	+ prop: color / bg / cursor / outline

# opacity
	+ 0 - 1

# navigation bar
  + là 1 list of links
	+ remove dấu đầu dòng, margin, padding
	  + list-style-type: none
	  + margin: 0
	  + padding: 0  REMOVE BROWSER DEFAULT SETTINGS 

  + vertical navigation
	+ set a -> block element (width, margin,padding,...)
	  + block sẽ chiếm toàn bộ chiều rộng có sẵn
	  + có thể set width cho 'ul' thay cho 'a'

	+ decor cho navigation
	  + hover, active
	  + text center cho 'a' or 'li'
	  + border / height
	  + cố dịnh vị trí -> fixed
	  + overflow khi có nhiều content trên bar

  + horizontal navigation
	+ using inline or float
	  + inline list item
		+ inline cho 'li' ('li' là block)

	  + float
		+ float cho li
		+ display block cho a
		+ BG-COLOR CHO 'UL' THAY VÌ 'A' ĐỂ CÓ BG FULL WIDTH

	  + decor ...
		  + sticky
			  top: 0
			  position: sticky

# dropdown
  + element cha thì relative
	  + element con thì absolute
		  + display default là none
		  + decor
  + khi hover vào thì display block

# form
	+ input field
		width
		type: text/pws/number
		thêm margin khi có nhiều input
		border
		bg-color / bg-image(icon)
		resize: none để ngăn việc biến đổi grabber

# counter
	+ giống tự động tăng
	+ counter-reset: 
	+ counter-increment
	+ content
	+ counter()

# unit
	+ em / rem / vw / vh / %

# rounded corners
    + border-radius

# border img
    + border-image: source[url()] slice width outset repeat
        + slice
        + outset
        + repeat

# bg- multi-bg
    + background: url() position repeat, url() position repeat
    + bg-size:
        + contain / cover
        + multi-bg-img
            + dùng ","
    +bg-clip

# color
    + opacity

# color key
    + transparent
    + currentcolor
    + inherit

# grandients
    + linear
        + linear-gradient(direction, color-stop1, color-stop2,...)
            + direction:
                + top -> bottom(default)
                    linear-gradient(red, yellow)
                + left to right
                    linear-gradient(to right, red, yellow)
                + diagonal(dg chéo)
                    linear-gradient(to bottom right, red, yellow)
                + use angle
                    linear-gradient(angle, red, yellow)
    + radial gradients
        + radial-gradient(shape size at position, start-color,..., last-color)
            + default: shape is ellipse / size: farthest-corner / position: center
            + size:
                + closest-side
                + farthest-side
                + closest-corner
                + farthest-corner
    + conic gradients
        + màu transition qyau xung quanh điểm center
        + conic-gradient([from angle] [at position] color [degree], color [degree],...)
            + default angle: 0deg / position: center


# shadow effect
    + text-shadow
        + text-shadow: ngang dọc blur color;
        + multi shadow:
            + text-shadow: set1, set2;
    + box-shadow
        + box-shadow: ngang dọc blur spread-radius color inset[or-not];
        + multi shadow:
            + box-shadow: set1, set2;



# text effect

    + text-overflow:
        + clip: phần dư bị cắt mất
        + ellipsis: phần dư thay = ...
        + visible:

    + word-wrap
        + ngắt chữ
        + word-wrap: break-word / 

    + word-break -> keep-all / break-all
    
    + writing-mode 

# web font

# 2d trans
    + transform
        + translate(x-axis, y-axis)
            + di chuyển element từ curr position
        + rotate(deg)
            + quay theo góc
        + scaleX(x)
            + tăng or giảm size theo chiều ngang
        + scaleY(y)
            + tăng or giảm size theo chiều dọc
        + scale(x,y)
        + skewX
            + góc nghiêng x
        + skewY
        + skew
        + matrix(scaleX, skewY, skewX, scaleY, translateX, translateY)

# 3d trans
    + method
        + rotateY(deg)
        + rotateX(deg)
        + rotateZ(deg)
    + prop
        + perspective
        + backface-visibility

# transition
    + transition-delay
    + transition-duration   default = 0s
    + transition-property
    + transition-timing-function

# animation
    + @keyframes
        @keyframes Ani-name{
            0% {...}
            25% {...}
            50% {...}
            100% {...}
        }
    + animation-name
    + animation-duration
    + animation-delay
    + animation-iteration-count
        + set số lần chạy: 1, 2, infinite
    + animation-direction
        + normal
        + reverse
        + alternate: đi xuôi xong đi ngược
        + alternate-reverse
    + animation-timing-function
        + linear / ease / ease-in / ease-out / ease-in-out
    + animation-fill-mode
        + none / forwards / backwards / both
    + animation
        (name duration fn delay count direction)


# object-fit
    + thay đổi size của img or video
    + prop
        + fill
        + contain
        + cover
        + none
        + scle-down

		
====================================================================
==========NOT CONFICT===============================================
====================================================================
# z-index
	chỉ được gán cho thẻ có khai báo position:absolute
	2 thẻ có cùng z-index: thẻ nằm dưới thì hiển thị phía trên, con nằm trên cha
# clearfix
	điều chỉnh vùng ko gian của thẻ cha so với thẻ con có dùng float(dùng float thì chiều cao của thẻ cha là 0px so với thẻ con float đó - chiều cao của thẻ cha sẻ được tăng lên khi nội dung bên trong nó ko sử dụng float)
	dùng clear:both vào after

  
# add css
	+ external
	+ internal
	+ inline

