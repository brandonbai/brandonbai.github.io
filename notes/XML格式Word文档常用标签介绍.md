---
layout: default
---

>Office2003以上，Word是可以以XML文本格式存储的。当需要在程序中通过操作XML文本的方式修改Word文档时，了解一下常用标签是很有必要的。

### 常用标签
名称|描述
-|-
w:p|文本段落
w:pPr|段落设置
w:ind|缩进
w:jc|文本位置(left/center/right/...)
w:r|文字块
w:rPr|文本设置
w:rFonts|字体设置
w:color|文字颜色
w:sz|文字大小
w:t|文本内容
w:b|粗体
w:i|斜体
w:u|下划线
w:strike|删除线
w:tbl|表格
w:tblPr|表格设置
w:tblGrid|单元格
w:tr|表格行
w:tc|表格列
w:tcPr|表格列设置
w:tcW|列宽


### word 样例

![样例.png](https://upload-images.jianshu.io/upload_images/5151732-7741749c5663ea4d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### XML 样例
```xml
<w:p w14:paraId="50DBBD76" w14:textId="77777777" w:rsidP="00CF041F" w:rsidR="00CF041F" w:rsidRDefault="00CF041F" w:rsidRPr="00CF041F">
	<w:pPr>
		<w:widowControl/>
		<w:shd w:color="auto" w:fill="FFFFFF" w:val="clear"/>
		<w:spacing w:line="360" w:lineRule="atLeast"/>
		<w:ind w:firstLine="480"/>
		<w:jc w:val="left"/>
		<w:rPr>
			<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
	</w:pPr>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>Microsoft Office Word</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>是</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
			<w:color w:val="136EC2"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>微软公司</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>的一个文字</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="SimSun" w:cs="SimSun" w:eastAsia="SimSun" w:hAnsi="SimSun"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>处</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>理器</w:t>
	</w:r>
	<w:hyperlink r:id="rId5" w:history="1" w:tgtFrame="_blank">
		<w:r w:rsidRPr="00CF041F">
			<w:rPr>
				<w:rFonts w:ascii="SimSun" w:cs="SimSun" w:eastAsia="SimSun" w:hAnsi="SimSun"/>
				<w:color w:val="136EC2"/>
				<w:sz w:val="21"/>
				<w:szCs w:val="21"/>
			</w:rPr>
			<w:t>应用程序</w:t>
		</w:r>
	</w:hyperlink>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>。</w:t>
	</w:r>
</w:p>
<w:p w14:paraId="19002BF0" w14:textId="77777777" w:rsidP="00CF041F" w:rsidR="00CF041F" w:rsidRDefault="00CF041F" w:rsidRPr="00CF041F">
	<w:pPr>
		<w:widowControl/>
		<w:shd w:color="auto" w:fill="FFFFFF" w:val="clear"/>
		<w:spacing w:line="360" w:lineRule="atLeast"/>
		<w:ind w:firstLine="480"/>
		<w:jc w:val="left"/>
		<w:rPr>
			<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
	</w:pPr>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
			<w:b/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>它</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
			<w:i/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>最</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
			<w:u w:val="single"/>
		</w:rPr>
		<w:t>初</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
			<w:strike/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>是</w:t>
	</w:r>
	<w:bookmarkStart w:id="0" w:name="_GoBack"/>
	<w:bookmarkEnd w:id="0"/>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>由</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>Richard Brodie</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="SimSun" w:cs="SimSun" w:eastAsia="SimSun" w:hAnsi="SimSun"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>为了</w:t>
	</w:r>
	<w:hyperlink r:id="rId6" w:history="1" w:tgtFrame="_blank">
		<w:r w:rsidRPr="00CF041F">
			<w:rPr>
				<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
				<w:color w:val="136EC2"/>
				<w:sz w:val="21"/>
				<w:szCs w:val="21"/>
			</w:rPr>
			<w:t>运行</w:t>
		</w:r>
	</w:hyperlink>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>DOS</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>的</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>IBM</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="SimSun" w:cs="SimSun" w:eastAsia="SimSun" w:hAnsi="SimSun"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>计算机而在</w:t>
	</w:r>
	<w:hyperlink r:id="rId7" w:history="1" w:tgtFrame="_blank">
		<w:r w:rsidRPr="00CF041F">
			<w:rPr>
				<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
				<w:color w:val="136EC2"/>
				<w:sz w:val="21"/>
				<w:szCs w:val="21"/>
			</w:rPr>
			<w:t>1983</w:t>
		</w:r>
		<w:r w:rsidRPr="00CF041F">
			<w:rPr>
				<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
				<w:color w:val="136EC2"/>
				<w:sz w:val="21"/>
				<w:szCs w:val="21"/>
			</w:rPr>
			<w:t>年</w:t>
		</w:r>
	</w:hyperlink>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="SimSun" w:cs="SimSun" w:eastAsia="SimSun" w:hAnsi="SimSun"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>编写的。随后的版本可运行于</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>Apple Macintosh (1984</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>年</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>)</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>、</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>SCO UNIX</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>和</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>Microsoft Windows (1989</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>年</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>)</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>，并成</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="SimSun" w:cs="SimSun" w:eastAsia="SimSun" w:hAnsi="SimSun"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>为</w:t>
	</w:r>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>了</w:t>
	</w:r>
	<w:hyperlink r:id="rId8" w:history="1" w:tgtFrame="_blank">
		<w:r w:rsidRPr="00CF041F">
			<w:rPr>
				<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
				<w:color w:val="136EC2"/>
				<w:sz w:val="21"/>
				<w:szCs w:val="21"/>
			</w:rPr>
			<w:t>Microsoft Office</w:t>
		</w:r>
	</w:hyperlink>
	<w:r w:rsidRPr="00CF041F">
		<w:rPr>
			<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
			<w:color w:val="333333"/>
			<w:sz w:val="21"/>
			<w:szCs w:val="21"/>
		</w:rPr>
		<w:t>的一部分。</w:t>
	</w:r>
</w:p>
<w:tbl>
	<w:tblPr>
		<w:tblStyle w:val="a4"/>
		<w:tblW w:type="auto" w:w="0"/>
		<w:tblLook w:firstColumn="1" w:firstRow="1" w:lastColumn="0" w:lastRow="0" w:noHBand="0" w:noVBand="1" w:val="04A0"/>
	</w:tblPr>
	<w:tblGrid>
		<w:gridCol w:w="4145"/>
		<w:gridCol w:w="4145"/>
	</w:tblGrid>
	<w:tr w14:paraId="703E7C85" w14:textId="77777777" w:rsidR="00CF041F" w:rsidTr="00CF041F">
		<w:tc>
			<w:tcPr>
				<w:tcW w:type="dxa" w:w="4145"/>
			</w:tcPr>
			<w:p w14:paraId="36A26862" w14:textId="77777777" w:rsidP="00CF041F" w:rsidR="00CF041F" w:rsidRDefault="00CF041F">
				<w:pPr>
					<w:widowControl/>
					<w:spacing w:line="390" w:lineRule="atLeast"/>
					<w:jc w:val="left"/>
					<w:rPr>
						<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
						<w:color w:val="333333"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
				</w:pPr>
				<w:r w:rsidRPr="00CF041F">
					<w:rPr>
						<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
						<w:b/>
						<w:bCs/>
						<w:color w:val="999999"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
					<w:t>原版名称</w:t>
				</w:r>
			</w:p>
		</w:tc>
		<w:tc>
			<w:tcPr>
				<w:tcW w:type="dxa" w:w="4145"/>
			</w:tcPr>
			<w:p w14:paraId="0F8B5B69" w14:textId="77777777" w:rsidP="00CF041F" w:rsidR="00CF041F" w:rsidRDefault="00CF041F">
				<w:pPr>
					<w:widowControl/>
					<w:spacing w:line="390" w:lineRule="atLeast"/>
					<w:jc w:val="left"/>
					<w:rPr>
						<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
						<w:color w:val="333333"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
				</w:pPr>
				<w:r w:rsidRPr="00CF041F">
					<w:rPr>
						<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
						<w:color w:val="333333"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
					<w:t>Microsoft office Word</w:t>
				</w:r>
			</w:p>
		</w:tc>
	</w:tr>
	<w:tr w14:paraId="4F0BE6C5" w14:textId="77777777" w:rsidR="00CF041F" w:rsidTr="00CF041F">
		<w:tc>
			<w:tcPr>
				<w:tcW w:type="dxa" w:w="4145"/>
			</w:tcPr>
			<w:p w14:paraId="283BEF0E" w14:textId="77777777" w:rsidP="00CF041F" w:rsidR="00CF041F" w:rsidRDefault="00CF041F">
				<w:pPr>
					<w:widowControl/>
					<w:spacing w:line="390" w:lineRule="atLeast"/>
					<w:jc w:val="left"/>
					<w:rPr>
						<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
						<w:color w:val="333333"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
				</w:pPr>
				<w:r w:rsidRPr="00CF041F">
					<w:rPr>
						<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
						<w:b/>
						<w:bCs/>
						<w:color w:val="999999"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
					<w:t>开</w:t>
				</w:r>
				<w:r w:rsidRPr="00CF041F">
					<w:rPr>
						<w:rFonts w:ascii="SimSun" w:cs="SimSun" w:eastAsia="SimSun" w:hAnsi="SimSun"/>
						<w:b/>
						<w:bCs/>
						<w:color w:val="999999"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
					<w:t>发</w:t>
				</w:r>
				<w:r w:rsidRPr="00CF041F">
					<w:rPr>
						<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
						<w:b/>
						<w:bCs/>
						<w:color w:val="999999"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
					<w:t>商</w:t>
				</w:r>
			</w:p>
		</w:tc>
		<w:tc>
			<w:tcPr>
				<w:tcW w:type="dxa" w:w="4145"/>
			</w:tcPr>
			<w:p w14:paraId="1E4EC5ED" w14:textId="77777777" w:rsidP="00CF041F" w:rsidR="00CF041F" w:rsidRDefault="00CF041F">
				<w:pPr>
					<w:widowControl/>
					<w:spacing w:line="390" w:lineRule="atLeast"/>
					<w:jc w:val="left"/>
					<w:rPr>
						<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
						<w:color w:val="333333"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
				</w:pPr>
				<w:r w:rsidRPr="00CF041F">
					<w:rPr>
						<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
						<w:color w:val="333333"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
					<w:t>微</w:t>
				</w:r>
				<w:r w:rsidRPr="00CF041F">
					<w:rPr>
						<w:rFonts w:ascii="SimSun" w:cs="SimSun" w:eastAsia="SimSun" w:hAnsi="SimSun"/>
						<w:color w:val="333333"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
					<w:t>软</w:t>
				</w:r>
				<w:r w:rsidRPr="00CF041F">
					<w:rPr>
						<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
						<w:color w:val="333333"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
					<w:t>（</w:t>
				</w:r>
				<w:r w:rsidRPr="00CF041F">
					<w:rPr>
						<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
						<w:color w:val="333333"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
					<w:t>Microsoft</w:t>
				</w:r>
				<w:r w:rsidRPr="00CF041F">
					<w:rPr>
						<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
						<w:color w:val="333333"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
					<w:t>）</w:t>
				</w:r>
			</w:p>
		</w:tc>
	</w:tr>
	<w:tr w14:paraId="7C66402F" w14:textId="77777777" w:rsidR="00CF041F" w:rsidTr="00CF041F">
		<w:tc>
			<w:tcPr>
				<w:tcW w:type="dxa" w:w="4145"/>
			</w:tcPr>
			<w:p w14:paraId="16A0ECF5" w14:textId="77777777" w:rsidP="00CF041F" w:rsidR="00CF041F" w:rsidRDefault="00CF041F">
				<w:pPr>
					<w:widowControl/>
					<w:spacing w:line="390" w:lineRule="atLeast"/>
					<w:jc w:val="left"/>
					<w:rPr>
						<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
						<w:color w:val="333333"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
				</w:pPr>
				<w:r w:rsidRPr="00CF041F">
					<w:rPr>
						<w:rFonts w:ascii="SimSun" w:cs="SimSun" w:eastAsia="SimSun" w:hAnsi="SimSun"/>
						<w:b/>
						<w:bCs/>
						<w:color w:val="999999"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
					<w:t>发行日</w:t>
				</w:r>
				<w:r w:rsidRPr="00CF041F">
					<w:rPr>
						<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
						<w:b/>
						<w:bCs/>
						<w:color w:val="999999"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
					<w:t>期</w:t>
				</w:r>
			</w:p>
		</w:tc>
		<w:tc>
			<w:tcPr>
				<w:tcW w:type="dxa" w:w="4145"/>
			</w:tcPr>
			<w:p w14:paraId="36AF413B" w14:textId="77777777" w:rsidP="00CF041F" w:rsidR="00CF041F" w:rsidRDefault="00CF041F">
				<w:pPr>
					<w:widowControl/>
					<w:spacing w:line="390" w:lineRule="atLeast"/>
					<w:jc w:val="left"/>
					<w:rPr>
						<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
						<w:color w:val="333333"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
				</w:pPr>
				<w:r w:rsidRPr="00CF041F">
					<w:rPr>
						<w:rFonts w:ascii="Arial" w:cs="Arial" w:eastAsia="Times New Roman" w:hAnsi="Arial"/>
						<w:color w:val="333333"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
					<w:t>1983</w:t>
				</w:r>
				<w:r w:rsidRPr="00CF041F">
					<w:rPr>
						<w:rFonts w:ascii="MS Mincho" w:cs="MS Mincho" w:eastAsia="MS Mincho" w:hAnsi="MS Mincho"/>
						<w:color w:val="333333"/>
						<w:sz w:val="18"/>
						<w:szCs w:val="18"/>
					</w:rPr>
					<w:t>年</w:t>
				</w:r>
			</w:p>
		</w:tc>
	</w:tr>
</w:tbl>

```
