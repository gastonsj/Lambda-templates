# A esta funcion se le debe agregar la politica para permitir "ecs:DescribeServices" y "ecs:UpdateService"
import boto3

def ChangeDesiredTask(cluster_name,service_name,desired):
    # Configura el cliente de ECS
    ecs_client = boto3.client('ecs')
    # Obtiene el recuento deseado actual del servicio
    response = ecs_client.describe_services(
        cluster=cluster_name,
        services=[service_name]
    )
    desired_count = response['services'][0]['desiredCount']
    print(f"Recuento deseado actual: {desired_count}")
    # Cambia el recuento deseado a n
    response = ecs_client.update_service(
        cluster=cluster_name,
        service=service_name,
        desiredCount=desired
    )
    # Obtiene el recuento deseado actualizado del servicio
    response = ecs_client.describe_services(
        cluster=cluster_name,
        services=[service_name]
    )
    desired_count = response['services'][0]['desiredCount']
    print(f"Recuento deseado actualizado: {desired_count}")

def lambda_handler(event, context):
    
    ChangeDesiredTask('prueba-matias','nginx',0)

    return {
        'statusCode': 200,
        'body': 'Recuento deseado cambiado con éxito'
    }
