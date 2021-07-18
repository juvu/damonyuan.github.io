# 5. Core Systems: Cards

1. [5.1 电子钱包的架构](https://www.kancloud.cn/jt_success/liuge/1513462)
2. 中国法律法规
   - 2010
     -《非金融机构支付服务管理办法》
   - 2013
     -《支付机构客户备付金存管办法》  
   - 2017
     -《关于进一步加强无证经营支付业务整治工作的通知》 -> [电商平台的“二清”模式解析](http://www.woshipm.com/it/3620624.html)
     -《关于实施支付机构客户备付金集中存管有关事项的通知》-> 备付金从商业银行转移到央行
   - 2018
     -《关于支付机构客户备付金全部集中交存有关事宜的通知》-> 2019年1月14日之前实现备付金100%集中交存央行  
3. [银行业务中的清算和结算分别是什么样的过程？](https://www.zhihu.com/question/19892912)
4. In the United States, interchange flows from the acquiring bank to the issuing bank on purchase transactions. As such, interchange is an expense to the acquiring bank and revenue to the card issuing bank. (Note that interchange on ATM transactions flows in reverse—the card issuer pays an interchange fee to the ATM deployer for servicing the issuer’s cardholder.)

5. merchant discount fee includes
   - interchange
   - network assessments and fees
   - others

6. Risk Management

  - KYC before create an account
  - Manage Authentication and Authorization
  - Manage Fraud
    - check the line items in an order and the ammount along with the timestamp
  - Manage Overdraft if pay through balance

7. E-commerce workflow

   1. cart
   2. checkout and generate an order
   3. confirm address, discount, payment method and update the order
   4. submit the order with line items
   5. risk management
   6. prepare payment gateway
   7. do the transaction
   8. record the transaction and journaling it into accounts
   9. reconciliation by the end of the day

# TODO

3. [支付系统会计记账设计](https://www.jianshu.com/p/186e72ad5573)     

4. [支付架构](https://zhouj000.github.io/tags/#%E6%94%AF%E4%BB%98%E6%9E%B6%E6%9E%84)

5. [支付系统的核心,账务系统都需要有哪些功能](https://zhuanlan.zhihu.com/p/293537477)