# 자바스크립트를 통한 사진 처리 기능  
# 프로젝트 소개
> 이 프로젝트는 자바스크립트의 canvas를 이용하여, 사진을 처리하는 여러 가지 기법을 다룹니다. 다양한 화소점 처리, 기하학 처리, 화소영역 처리, 그리고 히스토그램 처리 기법을 구현하여 이미지를 다양하게 가공할 수 있습니다.  

# deploy 주소
## https://janathanni.github.io/javascript-miniproject/

# 기능  <br>
##  화소점 처리
> 화소점 처리는 다른 화소의 영향 없이, 화소점의 값만 변경하는 것을 의미합니다.  

### 1. 밝기 조절
이미지 밝기 조절은 이미지의 픽셀값들을 증가시켜서 전체적으로 밝게, 혹은 감소시켜서 전체적으로 어둡게 만드는 작업입니다. 이를 통해 이미지의 세부사항을 조절할 수 있습니다.
```
        function add_image() {
            outH = inH;
            outW = inW;

            outImage = new Array(outH);
            for (var i = 0; i < outH; i++)
                outImage[i] = new Array(outW);
            
            var value = parseInt(prompt("값", "50"));
            for (var i = 0; i < inH; i++) {
                for (var k = 0; k < inW; k++) {
                    if (inImage[i][k] + value < 0)
                        outImage[i][k] = 0;
                    else if (inImage[i][k] + value > 255)
                        outImage[i][k] = 255;
                    else
                        outImage[i][k] = inImage[i][k] + value;
                }
            }
            displayImage();
        }
```
### 2. 반전
이미지 밝기 반전은 이미지의 밝은 부분을 어둡게, 어두운 부분을 밝게 반전시키는 작업입니다. 이를 통해 이미지의 대비를 높이는 효과를 가져올 수 있습니다.
```
        function reverse_image() {
            outH = inH;
            outW = inW;
            
            outImage = new Array(outH);
            for (var i = 0; i < outH; i++)
                outImage[i] = new Array(outW);
                
            for (var i = 0; i < inH; i++) {
                for (var k = 0; k < inW; k++) {
                    outImage[i][k] = 255 - inImage[i][k];
                }
            }
            displayImage();
        }

```
### 3. 흑백 처리
이미지 흑백화는 이미지를 흑백으로 변환하는 작업입니다. 이를 통해 이미지의 색상 정보를 제거하고, 명암 정보만을 남기는 것으로, 이미지를 단순화하여 처리할 때 유용합니다. 흑백화는 대부분의 컴퓨터 비전 알고리즘에서 사용됩니다.
```
        function bw3_image() {
            outH = inH;
            outW = inW;

            outImage = new Array(outH);
            for (var i = 0; i < outH; i++)
                outImage[i] = new Array(outW);

            var centerValue = 0;
            var oneAry = new Array(inH * inW);
            var index = 0;
            for (var i = 0; i < inH; i++)
                for (var k = 0; k < inW; k++)
                    oneAry[index++] = inImage[i][k];
            oneAry.sort();
            centerValue = oneAry[parseInt((inH * inW) / 2)];

            for (var i = 0; i < inH; i++) {
                for (var k = 0; k < inW; k++) {
                    if (inImage[i][k] <= centerValue)
                        outImage[i][k] = 0;
                    else
                        outImage[i][k] = 255;
                }
            }
            displayImage();
        }
```

## 기하학 처리
> 기하학 처리는 영상 내에 있는 화소들의 배치를 변경하는 것을 의미합니다. 영상의 회전, 확대 및 축소가 이에 해당합니다.

### 1. 축소
이미지의 크기를 줄이는 것으로, 이미지의 픽셀 값을 감소시키는 방법입니다. 이미지 크기를 줄이면 이미지가 더욱 거칠게 표현됩니다. 보간 방법을 사용하여 이미지를 축소할 수 있습니다.
```
        function zoomOut_image() {
            var scale = parseInt(prompt("축소배율", "2"));
            outH = parseInt(inH / scale);
            outW = parseInt(inW / scale);
            
            outImage = new Array(outH);
            for (var i = 0; i < outH; i++)
                outImage[i] = new Array(outW);
                
            outCanvas.height = outH;
            outCanvas.width = outW;
            
            for (var i = 0; i < inH; i++) {
                for (var k = 0; k < inW; k++) {
                    outImage[parseInt(i / scale)][parseInt(k / scale)] = inImage[i][k];
                }
            }
            displayImage();
        }
```
### 2. 확대
이미지의 크기를 확대하는 것으로, 이미지의 픽셀 값을 증가시키는 방법입니다. 이를 통해 이미지가 더욱 세밀하게 표현됩니다. 백워딩 확대는 보간(interpolation) 방법을 사용하여 이미지의 해상도를 높이는 방법입니다.
```
        function zoomIn2_image() {
            var scale = parseInt(prompt("확대배율", "2"));
            outH = parseInt(inH * scale);
            outW = parseInt(inW * scale);
            
            outImage = new Array(outH);
            for (var i = 0; i < outH; i++)
                outImage[i] = new Array(outW);
                
            outCanvas.height = outH;
            outCanvas.width = outW;
            for (var i = 0; i < outH; i++) {
                for (var k = 0; k < outW; k++) {
                    outImage[i][k] = inImage[parseInt(i / scale)][parseInt(k / scale)];
                }
            }
            displayImage();
        }
```
### 3. 회전
이미지를 일정한 각도만큼 회전시키는 것입니다. 중앙 회전은 이미지의 중심을 중심으로 회전시키는 것이고, 백워딩 회전은 이미지를 회전시킨 후 원래 위치로 돌려놓는 것입니다. 회전 변환은 회전 중심, 회전 각도, 보간 방법 등을 설정할 수 있습니다. 회전 시 이미지의 일부가 잘리거나 빈 공간이 생길 수 있으므로, 이를 방지하기 위해 이미지의 크기를 조정하는 등의 후처리가 필요할 수 있습니다.
```
    function rotate2_image() {
            outH = inH;
            outW = inW;
            
            outImage = new Array(outH);
            for (var i = 0; i < outH; i++)
                outImage[i] = new Array(outW);
                
            var angle = parseInt(prompt("각도", "45"));
            angle = angle * Math.PI / 180;
            
            var cx = parseInt(inH / 2);
            var cy = parseInt(inW / 2);

            for (var i = 0; i < outH; i++) {
                for (var k = 0; k < outW; k++) {
                    var old_i = parseInt(Math.cos(angle) * (i - cx) + Math.sin(angle) * (k - cy) + cx);
                    var old_k = parseInt(-Math.sin(angle) * (i - cx) + Math.cos(angle) * (k - cy) + cy);
                    if (((0 <= old_i) && (old_i < inH)) && ((0 <= old_k) && (old_k < inW))) {
                        outImage[i][k] = inImage[old_i][old_k];
                    }
                }
            }
            displayImage();
        }
```
## 화소영역 처리
> 화소영역 처리는 화소의 값만을 변경하는 처리가 아니라, 그 주위의 화소값도 함께 고려하는 것을 의미합니다.

### 1. 엠보싱
엠보싱은 이미지의 경계선을 강조하고 입체감을 부여하기 위해 사용되는 필터링 기법입니다. 이미지의 각 화소에 대해 주변의 화소값을 이용하여 새로운 화소값을 계산합니다. 계산된 화소값을 중심으로 상하 또는 좌우 방향으로 밝기가 강조된 모서리 효과를 만들어냅니다.
```
        function embos_image() {
            outH = inH;
            outW = inW;

            outImage = new Array(outH);
            for (var i = 0; i < outH; i++)
                outImage[i] = new Array(outW);

            var mask = [[-1.0, 0.0, 0.0],
            [0.0, 0.0, 0.0],
            [0.0, 0.0, 1.0]];
            var tmpInImage = new Array(inH + 2);
            for (var i = 0; i < inH + 2; i++)
                tmpInImage[i] = new Array(inW + 2);
                
            for (var i = 0; i < inH + 2; i++)
                for (var k = 0; k < inW + 2; k++)
                    tmpInImage[i][k] = 127.0;
                    
            for (var i = 0; i < inH; i++)
                for (var k = 0; k < inW; k++)
                    tmpInImage[i + 1][k + 1] = inImage[i][k];

            var tmpOutImage = new Array(outH);
            for (var i = 0; i < outH; i++)
                tmpOutImage[i] = new Array(outW);
                
            for (var i = 0; i < inH; i++) {
                for (var k = 0; k < inW; k++) {
                    var S = 0.0;
                    for (var m = 0; m < 3; m++)
                        for (var n = 0; n < 3; n++)
                            S += tmpInImage[i + m][k + n] * mask[m][n];

                    tmpOutImage[i][k] = S;
                }
            }
            for (var i = 0; i < outH; i++)
                for (var k = 0; k < outW; k++)
                    tmpOutImage[i][k] += 127.0;
            for (var i = 0; i < outH; i++)
                for (var k = 0; k < outW; k++)
                    outImage[i][k] = parseInt(tmpOutImage[i][k]);
            displayImage();
        }
```
### 2. 블러링
블러링은 이미지를 부드럽게 만들어주는 필터링 기법입니다. 이미지의 각 화소에 대해 주변의 화소값을 이용하여 새로운 화소값을 계산합니다. 계산된 화소값을 중심으로 노이즈를 제거하고 이미지를 흐리게 만들어줍니다.
```
        function blur_image() {
            outH = inH;
            outW = inW;
            
            outImage = new Array(outH);
            for (var i = 0; i < outH; i++)
                outImage[i] = new Array(outW);
                
            var mask = [[1 / 9.0, 1 / 9.0, 1 / 9.0],
            [1 / 9.0, 1 / 9.0, 1 / 9.0],
            [1 / 9.0, 1 / 9.0, 1 / 9.0]];
            
            var tmpInImage = new Array(inH + 2);
            for (var i = 0; i < inH + 2; i++)
                tmpInImage[i] = new Array(inW + 2);
                
            for (var i = 0; i < inH + 2; i++)
                for (var k = 0; k < inW + 2; k++)
                    tmpInImage[i][k] = 127.0;
                    
            for (var i = 0; i < inH; i++)
                for (var k = 0; k < inW; k++)
                    tmpInImage[i + 1][k + 1] = inImage[i][k];

            var tmpOutImage = new Array(outH);
            for (var i = 0; i < outH; i++)
                tmpOutImage[i] = new Array(outW);
                
            for (var i = 0; i < inH; i++) {
                for (var k = 0; k < inW; k++) {
                    var S = 0.0;
                    for (var m = 0; m < 3; m++)
                        for (var n = 0; n < 3; n++)
                            S += tmpInImage[i + m][k + n] * mask[m][n];

                    tmpOutImage[i][k] = S;
                }
            }
            
            for (var i = 0; i < outH; i++)
                for (var k = 0; k < outW; k++)
                    outImage[i][k] = parseInt(tmpOutImage[i][k]);
                    
            displayImage();
        }
```
### 3. 윤곽선 추출
윤곽선 추출(Edge detection): 윤곽선 추출은 이미지에서 경계선을 강조하여 추출하는 필터링 기법입니다. 주로 엣지 검출 알고리즘이 사용되며, 이미지의 각 화소에 대해 주변의 화소값을 이용하여 엣지를 찾아냅니다.
```
        function edge_image() {
            outH = inH;
            outW = inW;
            
            outImage = new Array(outH);
            for (var i = 0; i < outH; i++)
                outImage[i] = new Array(outW);
                
            var mask = [[0.0, -1.0, 0.0],
            [-1.0, 2.0, 0.0],
            [0.0, 0.0, 0.0]];
            
            var tmpInImage = new Array(inH + 2);
            for (var i = 0; i < inH + 2; i++)
                tmpInImage[i] = new Array(inW + 2);
                
            for (var i = 0; i < inH + 2; i++)
                for (var k = 0; k < inW + 2; k++)
                    tmpInImage[i][k] = 127.0;
                    
            for (var i = 0; i < inH; i++)
                for (var k = 0; k < inW; k++)
                    tmpInImage[i + 1][k + 1] = inImage[i][k];

            var tmpOutImage = new Array(outH);
            for (var i = 0; i < outH; i++)
                tmpOutImage[i] = new Array(outW);
                
            for (var i = 0; i < inH; i++) {
                for (var k = 0; k < inW; k++) {
                    var S = 0.0;
                    for (var m = 0; m < 3; m++)
                        for (var n = 0; n < 3; n++)
                            S += tmpInImage[i + m][k + n] * mask[m][n];

                    tmpOutImage[i][k] = S;
                }
            }
            for (var i = 0; i < outH; i++)
                for (var k = 0; k < outW; k++)
                    outImage[i][k] = parseInt(tmpOutImage[i][k]);
            displayImage();
        }
```
## 히스토그램 처리
> 히스토그램 처리는 히스토그램 정보를 이용하여, 화소값들의 분포도를 조정하는 것을 의미합니다.
### 1. 히스토그램 스트래칭
히스토그램 스트레칭은 이미지의 히스토그램에서 밝기 값의 분포를 늘리는 방식으로 이미지를 개선하는 기술입니다. 이 방식은 이미지의 전체 픽셀 값 범위를 이용하여 이미지의 대비를 개선합니다. 히스토그램 스트레칭을 적용하면 어두운 영역은 더욱 어두워지고 밝은 영역은 더욱 밝아집니다. 이 방식은 이미지의 밝기를 일정 수준 이상 조절해야 하는 경우에 사용할 수 있습니다.
```
        function histoSt_image() {
            outH = inH;
            outW = inW;
            
            outImage = new Array(outH);
            for (var i = 0; i < outH; i++)
                outImage[i] = new Array(outW);
                
            var low = inImage[0][0], high = inImage[0][0];
            for (var i = 0; i < inH; i++) {
                for (var k = 0; k < inW; k++) {
                    if (inImage[i][k] < low)
                        low = inImage[i][k];
                    if (inImage[i][k] > high)
                        high = inImage[i][k];
                }
            }
            for (var i = 0; i < inH; i++) {
                for (var k = 0; k < inW; k++) {
                    var out = ((inImage[i][k] - low) / (high - low) * 255.0);
                    outImage[i][k] = parseInt(out);
                }
            }
            displayImage();
        }
```
### 2. 엔드-인 탐색
엔드-인 탐색은 이미지의 히스토그램에서 특정 밝기 값에 집중하여 이미지의 대비를 개선하는 방식입니다. 이 방식은 이미지에서 가장 어두운 영역과 가장 밝은 영역을 개선합니다. 따라서 이 방식은 이미지의 대부분을 어둡게 만들지 않고 대비를 개선하는 데 적합합니다.
```
        function endIn_image() {
            outH = inH;
            outW = inW;
            
            outImage = new Array(outH);
            for (var i = 0; i < outH; i++)
                outImage[i] = new Array(outW);
                
            var low = inImage[0][0], high = inImage[0][0];
            for (var i = 0; i < inH; i++) {
                for (var k = 0; k < inW; k++) {
                    if (inImage[i][k] < low)
                        low = inImage[i][k];
                    if (inImage[i][k] > high)
                        high = inImage[i][k];
                }
            }
            low += 50;
            high -= 50;
            for (var i = 0; i < inH; i++) {
                for (var k = 0; k < inW; k++) {
                    var out = ((inImage[i][k] - low) / (high - low) * 255.0);
                    outImage[i][k] = parseInt(out);
                }
            }
            displayImage();
        }
```
### 3. 평활화
평활화는 이미지에서 밝기 값이 특정한 범위에 집중되어 있을 때 이를 균일하게 분포시키는 방식입니다. 이 방식은 이미지에서 특정한 밝기 값에 집중되어 있는 경우에 유용합니다. 평활화를 적용하면 이미지 전체의 대비가 개선되므로, 이미지의 세부 정보를 분석하기 쉬워집니다.
```
        function embos_image() {
            // (중요!) 출력 영상의 크기를 결정 --> 알고리즘에 따름.
            outH = inH;
            outW = inW;
            
            outImage = new Array(outH);
            for (var i = 0; i < outH; i++)
                outImage[i] = new Array(outW);
                
            var mask = [[-1.0, 0.0, 0.0],
            [0.0, 0.0, 0.0],
            [0.0, 0.0, 1.0]];
            
            var tmpInImage = new Array(inH + 2);
            for (var i = 0; i < inH + 2; i++)
                tmpInImage[i] = new Array(inW + 2);

            for (var i = 0; i < inH + 2; i++)
                for (var k = 0; k < inW + 2; k++)
                    tmpInImage[i][k] = 127.0;
                    
            for (var i = 0; i < inH; i++)
                for (var k = 0; k < inW; k++)
                    tmpInImage[i + 1][k + 1] = inImage[i][k];

            var tmpOutImage = new Array(outH);
            for (var i = 0; i < outH; i++)
                tmpOutImage[i] = new Array(outW);
                
            for (var i = 0; i < inH; i++) {
                for (var k = 0; k < inW; k++) {
                    var S = 0.0;
                    for (var m = 0; m < 3; m++)
                        for (var n = 0; n < 3; n++)
                            S += tmpInImage[i + m][k + n] * mask[m][n];

                    tmpOutImage[i][k] = S;
                }
            }
            for (var i = 0; i < outH; i++)
                for (var k = 0; k < outW; k++)
                    tmpOutImage[i][k] += 127.0;
                    
            for (var i = 0; i < outH; i++)
                for (var k = 0; k < outW; k++)
                    outImage[i][k] = parseInt(tmpOutImage[i][k]);
            displayImage();
        }
```
