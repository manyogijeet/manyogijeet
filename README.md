using UnityEngine;

public class MapSetup : MonoBehaviour
{
    public GameObject wallPrefab;
    public GameObject doorPrefab;
    public GameObject windowPrefab;
    public GameObject furniturePrefab;
    public GameObject lightPrefab;
    public GameObject keyItemPrefab;

    void Start()
    {
        CreateRoom(new Vector3(0, 0, 0), new Vector3(10, 3, 10)); // Main Room
        CreateRoom(new Vector3(15, 0, 0), new Vector3(6, 3, 6));   // Side Room
        PlaceDoor(new Vector3(5, 1, -5)); // Door between rooms
        PlaceWindow(new Vector3(2, 1, 5)); // Window in main room
        PlaceLight(new Vector3(0, 2.5f, 0)); // Central light in main room
        PlaceKeyItem(new Vector3(1, 0.5f, 1)); // Key item on table
    }

    void CreateRoom(Vector3 position, Vector3 size)
    {
        GameObject floor = GameObject.CreatePrimitive(PrimitiveType.Cube);
        floor.transform.position = position;
        floor.transform.localScale = new Vector3(size.x, 0.1f, size.z);

        // Walls
        Instantiate(wallPrefab, position + new Vector3(0, size.y / 2, size.z / 2), Quaternion.identity);
        Instantiate(wallPrefab, position + new Vector3(size.x / 2, size.y / 2, 0), Quaternion.Euler(0, 90, 0));
        Instantiate(wallPrefab, position + new Vector3(0, size.y / 2, -size.z / 2), Quaternion.identity);
        Instantiate(wallPrefab, position + new Vector3(-size.x / 2, size.y / 2, 0), Quaternion.Euler(0, 90, 0));
    }

    void PlaceDoor(Vector3 position)
    {
        Instantiate(doorPrefab, position, Quaternion.identity);
    }

    void PlaceWindow(Vector3 position)
    {
        Instantiate(windowPrefab, position, Quaternion.identity);
    }

    void PlaceLight(Vector3 position)
    {
        GameObject light = Instantiate(lightPrefab, position, Quaternion.identity);
        light.GetComponent<Light>().color = Color.red; // Eerie red light for horror ambiance
        light.GetComponent<Light>().intensity = 0.5f;
    }

    void PlaceKeyItem(Vector3 position)
    {
        Instantiate(keyItemPrefab, position, Quaternion.identity);
    }
}

 
