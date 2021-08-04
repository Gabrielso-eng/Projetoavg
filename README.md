import pandas as pd

** Leia o arquivo Salaries.csv como um DataFrame chamado "sal". **
sal = pd.read_csv('Salaries.csv')

** Verifique o "head" do DataFrame. **
sal.head()

** Use o método .info () para descobrir quantas entradas existem. **
sal.info()

** Qual é o "BasePay" médio? **
sal['BasePay'].mean()

** Qual é a maior quantidade de "OvertimePay" no conjunto de dados? **
sal['OvertimePay'].max()

** Qual é o cargo de JOSEPH DRISCOLL? Nota: use todas as maiúsculas, caso contrário você pode obter uma resposta que não coincida (há também um Joseph Driscoll com minúsculas). **
sal[sal['EmployeeName']=='JOSEPH DRISCOLL']['JobTitle']

** Quanto JOSEPH DRISCOLL ganha (incluindo benefícios)? **
sal[sal['EmployeeName']=='JOSEPH DRISCOLL']['TotalPayBenefits']

** Qual o nome da pessoa mais bem paga (incluindo benefícios)? **
sal[sal['TotalPayBenefits']== sal['TotalPayBenefits'].max()]
# ou
# sal.loc[sal['TotalPayBenefits'].idxmax()]

** Qual o nome da pessoa paga mais baixa (incluindo benefícios)? Você percebe algo estranho sobre o quanto ele ou ela é paga? **
sal[sal['TotalPayBenefits']== sal['TotalPayBenefits'].min()]

** Qual foi a média (média) BasePay de todos os funcionários por ano? (2011-2014)? **
sal.groupby('Year').mean()['BasePay']

** Quantos títulos de trabalho únicos existem? **
sal['JobTitle'].nunique()

** Quais são os 5 principais empregos mais comuns? **
sal['JobTitle'].value_counts().head(5)

** Quantos Títulos de Trabalho foram representados por apenas uma pessoa em 2013? (Por exemplo, títulos de trabalho com apenas uma ocorrência em 2013?) **
sum(sal[sal['Year']==2013]['JobTitle'].value_counts() == 1)

** Quantas pessoas têm a palavra Chefe em seu cargo? (Isso é bastante complicado) **
def chief_string(title):
    if 'chief' in title.lower():
        return True
    else:
        return False
        
sum(sal['JobTitle'].apply(lambda x: chief_string(x)))

** Bônus: Existe uma correlação entre o comprimento da seqüência do título do trabalho e o salário? **
sal['title_len'] = sal['JobTitle'].apply(len)
sal[['title_len','TotalPayBenefits']].corr() # Sem correlação


