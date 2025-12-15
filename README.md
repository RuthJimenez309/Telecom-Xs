# Telecom-Xs
print("\n" + "="*80)
print(" DISTRIBUCIÓN DE EVASIÓN (CHURN)")
print("="*80)

# Calcular distribución
churn_distribution = df_analysis['Eversion'].value_counts()
churn_percentage = df_analysis['Eversion'].value_counts(normalize=True) * 100

print(f"\n DISTRIBUCIÓN ABSOLUTA:")
print(churn_distribution)

print(f"\n DISTRIBUCIÓN PORCENTUAL:")
print(churn_percentage.round(2))

# Visualización
fig, axes = plt.subplots(1, 2, figsize=(14, 6))

# Gráfico de barras
axes[0].bar(churn_distribution.index, churn_distribution.values,
           color=['#2E8B57', '#DC143C'], alpha=0.8)
axes[0].set_title('Distribución de Evasión de Clientes', fontsize=16, fontweight='bold')
axes[0].set_xlabel('Estado del Cliente', fontsize=12)
axes[0].set_ylabel('Número de Clientes', fontsize=12)
axes[0].grid(True, alpha=0.3)

# Agregar valores en las barras
for i, v in enumerate(churn_distribution.values):
    axes[0].text(i, v + 50, str(v), ha='center', fontweight='bold')

# Gráfico de pastel
colors = ['#2E8B57', '#DC143C']
axes[1].pie(churn_percentage.values, labels=churn_percentage.index,
           autopct='%1.1f%%', colors=colors, startangle=90,
           textprops={'fontsize': 12})
axes[1].set_title('Porcentaje de Evasión', fontsize=16, fontweight='bold')

plt.tight_layout()
plt.show()

print(f"\n INSIGHT: {churn_percentage['se van']:.1f}% de los clientes han cancelado el servicio")
print(f" INSIGHT: La empresa pierde aproximadamente {churn_distribution['se van']} clientes")
