# convolution

- convolution의 의미: 필터의 모양을 이미지에 찍음 -> 블러, emboss, outline



# RGB image convolution

- 커널의 차원이 n * n *3이 됨
- feature map: convolution 채널이 여러개, output의 차원이 늘어남
- stack of conovlution: 여러개의 convolution을 거침, 
- 32 * 32* 3 의 이미지를 28 * 28 * 4 로 만들기 위해선 5 * 5 * 3 필터가 4개, 총 5 * 5 * 3 * 4 = 300개의 parameter가 필요함



# convolution neural network

- convolution layer: feature extraction
- pooling layer: feature extraction
- fully connected layer: decision making (ex. classification)
- 파라미터가 늘어나면 늘어날수록 새 데이터에 대한 성능이 나오지 않음
- 파라미터를 최대한 줄이는 방향으로 발전

 

# Stride

- 커널을 몇픽셀마다 찍을 것인가.



# Padding

- 필터가 가장자리에 찍힐 때 가장자리를 채워주는 역할
- zero padding
- input과 output의 차원이 똑같아 짐



# Convolution Arithmetic

- input size: 40 * 50 * 128, output size: 40 * 50 * 64
- padding (1), stride (1), 3 * 3 kernel
- 파라미터의 숫자는?
- 파라미터 숫자: 3 * 3 * 128 * 64 = 73728 



# 1 * 1 convolution

- 이미지를 줄이진 않고 dimension reduciton

- 레이어를 쌓으면서 패러미터를 줄이기 위해서

  