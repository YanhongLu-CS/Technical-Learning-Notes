I practice the use of pytorch in this folder.

Notebooks in "notebooks" folder are cloned from [pytorch offcial](https://docs.pytorch.org/tutorials/beginner/basics/intro.html)


关于data：
                 原始数据
                    ↓
    Dataset 负责“找到/取出一条数据”
                    ↓
    transform 负责“把这条数据加工成模型需要的样子”
                    ↓
    DataLoader 负责“把很多条加工后的数据打成 batch”
                    ↓
                   模型



关于搭建模型：

```
class NeuralNetwork(nn.Module):
    def __init__(self):
        super().__init__()
        self.flatten = nn.Flatten()
        self.linear_relu_stack = nn.Sequential(
            nn.Linear(28*28, 512),
            nn.ReLU(),
            nn.Linear(512, 512),
            nn.ReLU(),
            nn.Linear(512, 10),
        )

    def forward(self, x):
        x = self.flatten(x)
        logits = self.linear_relu_stack(x)
        return logits
```

用的时候直接：
`model(X)` 即可返回logits，不要直接调用model.forward()

```
model = NeuralNetwork().to(device)
print(model)
X = torch.rand(1, 28, 28, device=device)
logits = model(X)
pred_probab = nn.Softmax(dim=1)(logits)
y_pred = pred_probab.argmax(1)
print(f"Predicted class: {y_pred}")
```