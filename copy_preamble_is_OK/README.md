# Copy PreambleValue Part from IMF IAB to DCP IAB is OK

In the bitstream, there is only one part that is unknown, that is the ```PreambleValue```. ST 2098-2:2019 just tells us "Specification of the content of the payload is outside the scope of this specification", and it did not tell us where to find its definition.

Firstly, we tried to remove this part just by setting ```PreambleLength``` to ```0```, see ```RemovePreamble000002.atmos```. However, by merging frames with this operation, the finally generated DCP will not play Atmos well in Atmos Cinema. It could read the Atmos asset and activate Atmos playing mode, but it sounds really strange. By converting the merged Cinema MXF into ADM BWF and view in Dolby Atmos Renderer, we found out that every object's position was wrong. So we guess ```PreambleValue``` may contain something that represents the area.

However, in IMF IAB files, there is also a ```PreambleValue``` part. By comparing it with the same frame in original Cinema MXF, we found out there are just several bytes different. Then we tried to copy the ```PreambleValue``` from IMF IAB directly into Cinema MXF for each frame. Merge it and put into DCP, it works pretty fine.

Then we can copy the ```PreambleValue``` from IMF IAB directly, it is OK, although we don't know what is the difference. At least, my friend who tested the final Atmos copy processed with this step, he told me he could not tell the difference from the original Atmos DCP.

# 从IMF IAB中复制PreambleValue值到DCP IAB可行

在比特流中，只有一个部分是未知的，那就是```PreambleValue```值。ST 2098-2:2019告知我们，“该部分的内容规范不在本规范的定义范围内”，亦没有告知何处可获取此规范。

起初，我们尝试移除该部分通过简单地设置```PreambleLength```为```0```，见```RemovePreamble000002.atmos```。然而，在合并经过此操作的帧之后，最终成品DCP在全景声影院无法正常播放。全景声影院可以识别到全景声资源并以全景声状态播放内容，但听上去非常奇怪。通过转换合并的Cinema MXF为ADM BWF并在杜比全景声渲染器中播放，我们发现每一个声音对象的位置都错乱了。所以我们猜测```PreambleValue```可能记录了一些表示空间的信息。

然而，在IMF IAB文件中，同样有一个```PreambleValue```部分。通过对比它和同一Cinema MXF帧的此部分，我们发现它们只有几个字节不同。于是我们尝试直接复制IMF IAB中的```PreambleValue```值到Cinema MXF的每一对应帧中。合并并制作DCP，这次工作良好。

故此我们可以通过直接复制IMF IAB的```PreambleValue```值来解决此问题，尽管我们并不清楚这会造成什么差异。但至少，在影院测试最终成品的朋友称，他听不出来和官方原版的全景声有什么区别。
