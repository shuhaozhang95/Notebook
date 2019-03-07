# Activation function

{% embed url="https://blog.csdn.net/woaidapaopao/article/details/77806273" %}

<table>
  <thead>
    <tr>
      <th style="text-align:center">&#x6FC0;&#x6D3B;&#x51FD;&#x6570;</th>
      <th style="text-align:left">&#x516C;&#x5F0F;/&#x56FE;&#x50CF;</th>
      <th style="text-align:left">&#x7F3A;&#x70B9;</th>
      <th style="text-align:left">&#x4F18;&#x70B9;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:center">Sigmoid</td>
      <td style="text-align:left">
        <p></p>
        <p></p>
        <p>
          <img src="../.gitbook/assets/image (5).png" alt/>
        </p>
      </td>
      <td style="text-align:left">
        <p>1&#x3001;&#x4F1A;&#x6709;&#x68AF;&#x5EA6;&#x5F25;&#x6563;</p>
        <p></p>
        <p>2&#x3001;&#x4E0D;&#x662F;&#x5173;&#x4E8E;&#x539F;&#x70B9;&#x5BF9;&#x79F0;</p>
        <p></p>
        <p>3&#x3001;&#x8BA1;&#x7B97;exp&#x6BD4;&#x8F83;&#x8017;&#x65F6;</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:center">Tanh</td>
      <td style="text-align:left">
        <img src="../.gitbook/assets/tanh.jpg" alt/>
      </td>
      <td style="text-align:left">&#x68AF;&#x5EA6;&#x5F25;&#x6563;&#x6CA1;&#x6709;&#x89E3;&#x51B3;</td>
      <td
      style="text-align:left">1&#x3001;&#x89E3;&#x51B3;&#x4E86;&#x539F;&#x70B9;&#x5BF9;&#x79F0;&#x7684;&#x95EE;&#x9898;2&#x3001;&#x6BD4;Sigmoid&#x66F4;&#x5FEB;</td>
    </tr>
    <tr>
      <td style="text-align:center">ReLU</td>
      <td style="text-align:left">
        <img src="../.gitbook/assets/relu.jpg" alt/>
      </td>
      <td style="text-align:left">&#x68AF;&#x5EA6;&#x5F25;&#x6563;&#x6CA1;&#x5B8C;&#x5168;&#x89E3;&#x51B3;&#xFF0C;&#x5728;&#xFF08;-&#xFF09;&#x90E8;&#x5206;&#x76F8;&#x5F53;&#x4E8E;&#x795E;&#x7ECF;&#x6B7B;&#x4EA1;&#x800C;&#x4E14;&#x4E0D;&#x4F1A;&#x590D;&#x6D3B;</td>
      <td
      style="text-align:left">1&#x3001;&#x89E3;&#x51B3;&#x4E86;&#x90E8;&#x5206;&#x68AF;&#x5EA6;&#x5F25;&#x6563;&#x95EE;&#x9898;2&#x3001;&#x6536;&#x655B;&#x901F;&#x5EA6;&#x66F4;&#x5FEB;</td>
    </tr>
    <tr>
      <td style="text-align:center">Leaky ReLU</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x89E3;&#x51B3;&#x4E86;&#x795E;&#x7ECF;&#x6B7B;&#x4EA1;&#x7684;&#x95EE;&#x9898;</td>
    </tr>
    <tr>
      <td style="text-align:center">Maxout</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">&#x53C2;&#x6570;&#x6BD4;&#x8F83;&#x591A;&#xFF0C;&#x672C;&#x8D28;&#x4E0A;&#x662F;&#x5728;&#x8F93;&#x51FA;&#x7ED3;&#x679C;&#x4E0A;&#x53C8;&#x589E;&#x52A0;&#x4E86;&#x4E00;&#x5C42;</td>
      <td
      style="text-align:left">&#x514B;&#x670D;&#x4E86;ReLU&#x7684;&#x7F3A;&#x70B9;&#xFF0C;&#x6BD4;&#x8F83;&#x63D0;&#x5021;&#x4F7F;&#x7528;</td>
    </tr>
  </tbody>
</table>

