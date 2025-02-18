# Soccer Match Data Visualization in Unity

This Unity project visualizes soccer match data generated by Roboflow using homography transformation to map player positions from video frames to a 3D soccer pitch. The project supports real-time playback of match data, showing player and referee positions on the field based on the provided JSON data.

## Features

- **Player and Referee Tracking**: Displays the positions of players and referees on the pitch, with each player assigned to a team and color-coded accordingly.
- **Homography-based Mapping**: Uses homography transformation to map 2D positions from video data to a 3D Unity pitch.
- **Real-time Playback**: Simulates the game using data from recorded frames, with adjustable playback speed.
- **Pitch Scaling**: Adjust the pitch size in Unity to match real-world dimensions.

## Example of a Visualization
![image](https://github.com/user-attachments/assets/390d5dc7-210e-42f1-bffb-48d82ce6f745)


## Installation

### Prerequisites

- **Unity Version**: Unity 2020.3.49 is recommended.
- **Python**: The match data must be generated using Python scripts provided in the [project repository. Make sure to have Python installed along with required dependencies to generate the JSON data.](https://github.com/sssabet/RoboflowSport)

### Setup Instructions

1. **Clone the Repository**:  
   Clone this repository to your local machine using Git:
   ```bash
   git clone https://github.com/sssabet/AR-Unity-SoccerVision.git
   cd AR-Unity-SoccerVision
2. **Open the Unity Project**:
   - Open Unity Hub.
   - Click `Add`, then navigate to the folder where you cloned the repository.
   - Open the project in Unity.

3. **Import Required Assets**:
   - Ensure the `MathNet.Numerics` library is installed in Unity (for matrix operations). You can install this via the NuGet package manager or include the `DLL` files directly in the `Plugins` folder.
   - Add asset https://assetstore.unity.com/packages/3d/animations/basic-motions-free-154271 to the project or any similar humoniod asset
   - Add the matchdata and a video generated from the python script or use the provided example.

5. **Match Data Generation**:
   - Run the Python script to extract player tracking data and generate the `matchData.json` file.
   - Place the `matchData.json` and the video in the `Assets/Resources/` folder of your Unity project.

## Usage

### Running the Simulation

1. **Load Match Data**:
   - When the Unity scene is started, the `MatchDataLoader` script automatically loads the `matchData.json` file from the `Assets/Resources/` folder.

2. **Play the Simulation**:
   - Press `Play` in the Unity Editor to start the simulation. The players and referees will be animated according to the positions in each frame of the JSON data.

### Debugging

- Debug information about player positions and transformations will be displayed in Unity's console, including data about player movement and referee tracking.
- You can enable additional logging in the `MatchDataLoader.cs` script if needed.

### Encode video for Ubunto to Unity
```
ffmpeg -i input.mp4 -c:v libvpx -b:v 1M -pix_fmt yuv420p -g 120 -deadline good -cpu-used 0 -c:a libvorbis -b:a 128k output.webm
```

## JSON Data Structure

The `matchData.json` file stores the frames of the match with player and referee positions. The JSON data is generated by Roboflow's object detection and homography tools. Each frame contains a list of players, goalkeepers, and referees, along with their positions and team assignments. The structure is as follows:

```json
{
  "frames": [
    {
      "frame_index": 0,
      "players": [
        {"id": 1, "team_id": 0, "position": [123.0, 456.0]},
        {"id": 2, "team_id": 1, "position": [789.0, 321.0]}
      ],
      "goalkeepers": [
        {"id": 3, "team_id": 0, "position": [456.0, 654.0]}
      ],
      "referees": [
        {"position": [654.0, 987.0]}
      ]
    },
  ]
}
```

   - frame_index: The index of the frame (0-based).
   - players: List of player objects, each containing:
   - id: Unique identifier of the player.
   - team_id: Team ID (0 or 1).
   - position: The player's 2D position in video space coordinates.
   - goalkeepers: Similar to players but specifically for goalkeepers.
   - referees: A list of referees' positions (they don't have IDs in this version).


## Contributing

If you'd like to contribute to this project, feel free to fork the repository and submit a pull request. Any suggestions or improvements are welcome! 

Here are some ways you can contribute:

- **Bug Reports**: If you find any bugs, please report them using the Issues page on GitHub.
- **Feature Suggestions**: Have an idea for a new feature? Submit a feature request or suggest improvements.
- **Pull Requests**: Fix issues, improve existing code, or add new functionality — pull requests are highly appreciated!

Before making a large contribution, consider discussing it first by opening an issue to ensure it aligns with the project direction.

## Known Issues
- **Player Overlapping**: If multiple players are detected at the same position, they may overlap visually on the Unity pitch, which can make it difficult to differentiate between them.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

